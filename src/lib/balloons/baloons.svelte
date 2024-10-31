<script lang="ts">
	import { onMount } from 'svelte';

	let canvas: HTMLCanvasElement;
	let ctx: CanvasRenderingContext2D;
	let bCtx: CanvasRenderingContext2D;

	let cw: number, cx: number, ch: number, cy: number;
	let frames = 0;
	let requestId: number | null = null;
	const rad = Math.PI / 180;
	const kappa = 0.5522847498;
	let balloons: Balloon[] = [];

	class Balloon {
		r: number;
		R: number;
		x: number;
		y: number;
		a: number;
		pm: number;
		speed: number;
		k: number;
		hue: string;
		cx: number; // Adding cx property
		cy: number; // Adding cy property

		constructor() {
			this.r = randomIntFromInterval(20, 70);
			this.R = 1.4 * this.r;
			this.x = randomIntFromInterval(this.r, cw - this.r);
			this.y = ch + 2 * this.r;
			this.a = this.r * 4.5;
			this.pm = Math.random() < 0.5 ? -1 : 1;
			this.speed = randomIntFromInterval(1.5, 4);
			this.k = this.speed / 5;
			this.hue = this.pm > 0 ? '210' : '10';
			this.cx = 0; // Initializing cx
			this.cy = 0; // Initializing cy
		}
	}

	function Init() {
		if (requestId) {
			cancelAnimationFrame(requestId);
			requestId = null;
		}
		cw = canvas.width = window.innerWidth;
		ch = canvas.height = window.innerHeight + 100;
		cx = cw / 2;
		cy = ch;

		// Set the size of the off-screen canvas
		bCtx.canvas.width = cw;
		bCtx.canvas.height = ch;

		ctx.clearRect(0, 0, cw, ch);
		bCtx.strokeStyle = '#abcdef';
		bCtx.lineWidth = 1;
		Draw();
	}

	function Draw() {
		updateBalloons(bCtx);
		ctx.clearRect(0, 0, cw, ch);
		ctx.drawImage(bCtx.canvas, 0, 0);
		requestId = requestAnimationFrame(Draw);
	}

	function updateBalloons(ctx: CanvasRenderingContext2D) {
		frames += 1;
		if (frames % 37 === 0 && balloons.length < 37) {
			balloons.push(new Balloon());
		}
		ctx.clearRect(0, 0, cw, ch);

		for (const b of balloons) {
			if (b.y > -b.a) {
				b.y -= b.speed;
			} else {
				b.y = ch + b.r + b.R;
			}
			const p = thread(b, ctx);
			b.cx = p.x;
			b.cy = p.y - b.R;
			ctx.fillStyle = Grd(p.x, p.y, b.r, b.hue);
			drawBalloon(b, ctx);
		}
	}

	function drawBalloon(b: Balloon, ctx: CanvasRenderingContext2D) {
		const or = b.r * kappa;

		const p1 = { x: b.cx - b.r, y: b.cy };
		const pc11 = { x: p1.x, y: p1.y + or };
		const pc12 = { x: p1.x, y: p1.y - or };

		const p2 = { x: b.cx, y: b.cy - b.r };
		const pc21 = { x: b.cx - or, y: p2.y };
		const pc22 = { x: b.cx + or, y: p2.y };

		const p3 = { x: b.cx + b.r, y: b.cy };
		const pc31 = { x: p3.x, y: p3.y - or };
		const pc32 = { x: p3.x, y: p3.y + or };

		const p4 = { x: b.cx, y: b.cy + b.R };
		const pc41 = { x: p4.x + or, y: p4.y };
		const pc42 = { x: p4.x - or, y: p4.y };

		ctx.beginPath();
		ctx.moveTo(p4.x, p4.y);
		ctx.bezierCurveTo(pc42.x, pc42.y, pc11.x, pc11.y, p1.x, p1.y);
		ctx.bezierCurveTo(pc12.x, pc12.y, pc21.x, pc21.y, p2.x, p2.y);
		ctx.bezierCurveTo(pc22.x, pc22.y, pc31.x, pc31.y, p3.x, p3.y);
		ctx.bezierCurveTo(pc32.x, pc32.y, pc41.x, pc41.y, p4.x, p4.y);
		ctx.closePath();
		ctx.fill();
	}

	function thread(b: Balloon, ctx: CanvasRenderingContext2D) {
		let x = b.x,
			y = b.y;

		ctx.beginPath();
		for (let i = b.a; i > 0; i -= 1) {
			const t = i * rad;
			x = b.x + b.pm * 50 * Math.cos(b.k * t - frames * rad);
			y = b.y + b.pm * 25 * Math.sin(b.k * t - frames * rad) + 50 * t;
			ctx.lineTo(x, y);
		}
		ctx.stroke();
		return { x, y };
	}

	function Grd(x: number, y: number, r: number, hue: string) {
		const grd = ctx.createRadialGradient(x - 0.5 * r, y - 1.7 * r, 0, x - 0.5 * r, y - 1.7 * r, r);
		grd.addColorStop(0, `hsla(${hue},100%,65%,.95)`);
		grd.addColorStop(0.4, `hsla(${hue},100%,45%,.85)`);
		grd.addColorStop(1, `hsla(${hue},100%,25%,.80)`);
		return grd;
	}

	function randomIntFromInterval(min: number, max: number) {
		return Math.floor(Math.random() * (max - min + 1) + min);
	}

	onMount(() => {
		const c = canvas as HTMLCanvasElement;
		ctx = c.getContext('2d')!;
		const bc = document.createElement('canvas');
		bCtx = bc.getContext('2d')!;
		Init();
		window.addEventListener('resize', Init);
	});
</script>

<canvas bind:this={canvas} id="c"></canvas>

<style>
	@font-face {
		font-family: 'Monoton';
		src: url(https://themes.googleusercontent.com/static/fonts/monoton/v4/AKI-lyzyNHXByGHeOcds_w.woff)
			format('woff');
	}

	* {
		margin: 0;
		padding: 0;
		overflow: hidden;
		z-index: 100;
	}

	canvas {
		position: absolute;
		top: 0;
		left: 0;
		width: 100vw; /* Viewport width */
		height: 100vh; /* Viewport height */
	}

	body {
		background: radial-gradient(#fec215, #f8a90c);
	}

	.text {
		position: absolute;
		left: 0;
		top: 0;
		width: 100vw;
		font-size: 50px;
		text-align: center;
		margin-top: calc(30vh - 0.5em);
		font-family: Monoton;
		color: hsl(35, 100%, 84%);
		z-index: -1;
	}
</style>
