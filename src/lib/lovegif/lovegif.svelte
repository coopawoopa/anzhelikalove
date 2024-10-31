<script lang="ts">
	import { onMount } from 'svelte';

	onMount(() => {
		const wrapper = document.querySelector('.wrapper');
		const love = wrapper?.querySelector('.heart');

		// Check if wrapper and love elements exist before proceeding
		if (wrapper && love) {
			for (let i = 0; i < 4; i++) {
				const clone = love.cloneNode(true) as SVGElement;
				wrapper.appendChild(clone);
			}
		}
	});
</script>

<div class="wrapper">
	<!-- Heart SVG -->
	<svg class="heart" viewBox="0 0 101.7 87.6">
		<path
			d="M51,12.8c0-0.1-0.1-0.1-0.1-0.2c0,0.1-0.1,0.1-0.1,0.2C31-10.7,0,0.2,0,28.9c0,27.6,40.7,56.9,50.9,58.8
      c10.1-1.8,50.9-31.1,50.9-58.8C101.7,0.2,70.7-10.7,51,12.8z"
		/>
	</svg>
</div>

<style>
	/* Set background and overflow properties */

	:global(body) {
		width: 100%;
		height: 100%;
		background: #be1e2d;
		overflow: hidden;
		margin: 0;
	}

	.wrapper {
		position: relative;
		width: 100vw;
		height: 100vh;
	}

	/* Define the heart style and animation */
	.heart {
		width: 100%;
		height: 100%;
		position: absolute;
		top: 0;
		left: 0;
		opacity: 0;
		animation-name: radiate;
		animation-duration: 5s;
		animation-iteration-count: infinite;
		animation-timing-function: linear;
		animation-direction: normal;
		animation-fill-mode: backwards;
	}

	.heart path {
		fill: #fff;
	}

	/* Set animation delay for each cloned heart */
	.heart:nth-child(1) {
		animation-delay: -1s;
	}
	.heart:nth-child(2) {
		animation-delay: -2s;
	}
	.heart:nth-child(3) {
		animation-delay: -3s;
	}
	.heart:nth-child(4) {
		animation-delay: -4s;
	}
	.heart:nth-child(5) {
		animation-delay: -5s;
	}

	/* Define keyframes for radiate animation */
	@keyframes radiate {
		0% {
			opacity: 0;
			transform: scale(0);
		}
		1% {
			opacity: 0.15;
		}
		100% {
			opacity: 0;
			transform: scale(2);
		}
	}
</style>
