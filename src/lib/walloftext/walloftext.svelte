<script lang="ts">
	export let text: string = 'Я ТЕБЯ ЛЮБЛЮ'; // Phrase to repeat in each line
	export let lineCount: number = 25; // Number of lines in the wall

	// Helper function to generate alternating bold and normal text
	function generateAlternatingText(text: string, repetitions: number) {
		return Array.from({ length: repetitions }, (_, i) => ({
			text,
			bold: i % 2 === 0 // Make every other repetition bold
		}));
	}

	const repeatedText = generateAlternatingText(text, 50);
</script>

<div class="text-wall">
	{#each Array(lineCount) as _, i}
		<div class="line">
			{#each repeatedText as item}
				{#if i % 2 === 0}
					<span class={item.bold ? 'bold' : ''}>{item.text}&nbsp;</span>
				{:else}
					<span class={item.bold ? '' : 'bold'}>{item.text}&nbsp;</span>
				{/if}
			{/each}
		</div>
	{/each}
</div>

<style>
	.text-wall {
		position: fixed;
		top: 0;
		left: 0;
		width: 100%;
		height: 100vh;
		overflow: hidden;
		display: flex;
		flex-direction: column;
		justify-content: space-evenly;
		z-index: -1;
	}

	.line {
		white-space: nowrap;
		font-size: 2em;
		display: flex;
		justify-content: center;
		position: relative;
		width: 150vw;
		overflow: hidden;
		text-align: center;
		color: rgba(255, 39, 36, 0.431);
	}

	/* Style for bold text */
	.bold {
		font-weight: bold;
	}

	/* Oscillation animation for desktop screens */
	@keyframes oscillate {
		0% {
			transform: translateX(-10%);
		}
		50% {
			transform: translateX(0%);
		}
		100% {
			transform: translateX(-10%);
		}
	}

	/* Apply the oscillation animation with slight delay variations */
	.line:nth-child(odd) {
		animation: oscillate 12s ease-in-out infinite;
	}

	.line:nth-child(even) {
		animation: oscillate 15s ease-in-out infinite;
	}

	/* Adjust oscillation speed for smaller screens */
	@media (max-width: 768px) {
		@keyframes oscillate {
			0% {
				transform: translateX(-30%);
			}
			50% {
				transform: translateX(-10%);
			}
			100% {
				transform: translateX(-30%);
			}
		}
		.line:nth-child(odd) {
			animation: oscillate 8s ease-in-out infinite; /* Faster animation for mobile */
		}

		.line:nth-child(even) {
			animation: oscillate 10s ease-in-out infinite; /* Slightly faster for variation */
		}
	}
</style>
