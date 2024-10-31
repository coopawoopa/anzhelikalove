<script lang="ts">
	import { onMount } from 'svelte';

	let canvas: HTMLCanvasElement;
	let context: CanvasRenderingContext2D;
	let w: number;
	let h: number;
	const NUM_CONFETTI = 100;
	const COLORS = [
		[85, 71, 106],
		[174, 61, 99],
		[219, 56, 83],
		[244, 92, 68],
		[248, 182, 70]
	];
	const PI_2 = 2 * Math.PI;

	let xpos = 0.5;
	let confetti: Confetti[];

	function resizeWindow() {
		w = canvas.width = window.innerWidth;
		h = canvas.height = window.innerHeight;
	}

	class Confetti {
		x!: number;
		y!: number;
		r!: number;
		r2!: number;
		vx!: number;
		vy!: number;
		opacity!: number;
		dop!: number;
		xmax!: number;
		ymax!: number;
		rgb!: string;
		style!: number[];

		constructor() {
			this.style = COLORS[Math.floor(range(0, COLORS.length))];
			this.rgb = `rgba(${this.style[0]},${this.style[1]},${this.style[2]}`;
			this.r = Math.floor(range(2, 6));
			this.r2 = 2 * this.r;
			this.replace();
		}

		replace() {
			this.opacity = 0;
			this.dop = 0.03 * range(1, 4);
			this.x = range(-this.r2, w - this.r2);
			this.y = range(-20, h - this.r2);
			this.xmax = w - this.r;
			this.ymax = h - this.r;
			this.vx = range(0, 2) + 8 * xpos - 5;
			this.vy = 0.7 * this.r + range(-1, 1);
		}

		draw() {
			this.x += this.vx;
			this.y += this.vy;
			this.opacity += this.dop;
			if (this.opacity > 1) {
				this.opacity = 1;
				this.dop *= -1;
			}
			if (this.opacity < 0 || this.y > this.ymax) this.replace();
			if (!(0 < this.x && this.x < this.xmax)) this.x = (this.x + this.xmax) % this.xmax;
			drawCircle(this.x, this.y, this.r, `${this.rgb},${this.opacity})`);
		}
	}

	function range(a: number, b: number) {
		return (b - a) * Math.random() + a;
	}

	function drawCircle(x: number, y: number, r: number, style: string) {
		context.beginPath();
		context.arc(x, y, r, 0, PI_2, false);
		context.fillStyle = style;
		context.fill();
	}

	function step() {
		context.clearRect(0, 0, w, h);
		confetti.forEach((c) => c.draw());
		requestAnimationFrame(step);
	}

	onMount(() => {
		context = canvas.getContext('2d')!;
		resizeWindow();
		confetti = Array.from({ length: NUM_CONFETTI }, () => new Confetti());

		window.addEventListener('resize', resizeWindow);
		document.onmousemove = (e) => (xpos = e.pageX / w);
		requestAnimationFrame(step);
	});
</script>

<canvas bind:this={canvas} id="world"></canvas>

<canvas bind:this={canvas} id="world"></canvas>

<style>
	html,
	body {
		margin: 0;
		padding: 0;
		width: 100%;
		height: 100%;
		overflow: hidden;
		background: #111;
	}

	canvas {
		display: block;
		position: fixed; /* Change to fixed positioning */
		top: 0;
		left: 0;
		width: 100vw;
		height: 100vh;
		pointer-events: none; /* Optional: makes sure the confetti doesn’t interfere with clicks */
	}
</style>
