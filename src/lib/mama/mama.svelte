<script>
	// No JavaScript needed for this component
</script>

<div class="text-container">
	<svg viewBox="0 0 200 100">
		<!-- SVG Paths for each letter (M, A, M, A) -->
		<path d="M10,80 L30,10 L50,80 L70,10 L90,80" />
		<!-- M -->
		<path d="M110,80 Q130,10,150,80 Q130,50,110,80 Z" />
		<!-- A -->
		<path d="M170,80 L190,10 L210,80 L230,10 L250,80" />
		<!-- M -->
		<path d="M270,80 Q290,10,310,80 Q290,50,270,80 Z" />
		<!-- A -->
	</svg>
</div>

<style>
	.text-container {
		width: 100%;
		height: 100%;
		display: flex;
		align-items: center;
		justify-content: center;
		background-color: #222;
	}

	svg {
		width: 60%;
		height: auto;
	}

	path {
		fill: none;
		stroke: #f2a900; /* Brush stroke color */
		stroke-width: 6;
		stroke-linecap: round;
		stroke-linejoin: round;
		stroke-dasharray: 500; /* Adjust to control path length */
		stroke-dashoffset: 500; /* Starts the stroke offset, so it's invisible */
		animation: draw 2s ease forwards; /* Draws the path in 2 seconds */
	}

	/* Animation for drawing the stroke */
	@keyframes draw {
		to {
			stroke-dashoffset: 0; /* Animates the stroke offset from 500 to 0, "drawing" the path */
		}
	}

	/* Delay for each letter */
	path:nth-child(2) {
		animation-delay: 0.5s;
	}

	path:nth-child(3) {
		animation-delay: 1s;
	}

	path:nth-child(4) {
		animation-delay: 1.5s;
	}
</style>
