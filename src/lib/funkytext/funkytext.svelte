<script>
	// No JavaScript needed for this component
</script>

<h1>
	<span>С</span>
	<br />
	<span>Д</span>
	<span>Н</span>
	<span>Е</span>
	<span>М</span>
	<br />
	<span>Р</span>
	<span>О</span>
	<span>Ж</span>
	<span>Д</span>
	<span>Е</span>
	<span>Н</span>
	<span>И</span>
	<span>Я</span>
	<br />
	<span>М</span>
	<span>А</span>
	<span>М</span>
	<span>У</span>
	<span>Л</span>
	<span>Я</span>
</h1>

<style>
	@import url('https://fonts.googleapis.com/css?family=Luckiest+Guy');

	/* BODY */
	:global(html),
	:global(body) {
		margin: 0;
		padding: 0;
		width: 100%;
		height: 100%;
		overflow: hidden;

		background-attachment: fixed;
		background-size: 100% 100%;
		font-family: 'Luckiest Guy', cursive;
		-webkit-font-smoothing: antialiased;
	}

	::selection {
		background: transparent;
	}

	/* CLOUDS */
	:global(body):before {
		content: '';
		position: absolute;
		top: 0;
		left: 0;
		right: 0;
		width: 0;
		height: 0;
		margin: auto;
		border-radius: 100%;
		background: transparent;
		display: block;
		box-shadow:
			0 0 150px 100px rgba(255, 255, 255, 0.6),
			200px 0 200px 150px rgba(255, 255, 255, 0.6),
			-250px 0 300px 150px rgba(255, 255, 255, 0.6),
			550px 0 300px 200px rgba(255, 255, 255, 0.6),
			-550px 0 300px 200px rgba(255, 255, 255, 0.6);
	}

	/* JUMP */
	h1 {
		cursor: default;
		position: absolute;
		top: 0;
		left: 0;
		right: 0;
		bottom: 0;
		width: 100%;
		height: 100px;
		margin: auto;
		display: block;
		text-align: center;
	}

	h1 span {
		position: relative;
		top: -300px;
		display: inline-block;
		animation: bounce 0.3s ease infinite alternate;
		font-size: 50px;
		color: #fff;
		text-shadow:
			0 1px 0 #ccc,
			0 2px 0 #ccc,
			0 3px 0 #ccc,
			0 4px 0 #ccc,
			0 5px 0 #ccc,
			0 6px 0 transparent,
			0 7px 0 transparent,
			0 8px 0 transparent,
			0 9px 0 transparent,
			0 10px 10px rgba(0, 0, 0, 0.4);
	}

	/* Delay for each letter */
	h1 span:nth-child(2) {
		animation-delay: 0.1s;
	}
	h1 span:nth-child(3) {
		animation-delay: 0.2s;
	}
	h1 span:nth-child(4) {
		animation-delay: 0.3s;
	}
	h1 span:nth-child(5) {
		animation-delay: 0.4s;
	}
	h1 span:nth-child(6) {
		animation-delay: 0.5s;
	}
	h1 span:nth-child(7) {
		animation-delay: 0.6s;
	}
	h1 span:nth-child(8) {
		animation-delay: 0.2s;
	}
	h1 span:nth-child(9) {
		animation-delay: 0.3s;
	}
	h1 span:nth-child(10) {
		animation-delay: 0.4s;
	}
	h1 span:nth-child(11) {
		animation-delay: 0.5s;
	}
	h1 span:nth-child(12) {
		animation-delay: 0.6s;
	}
	h1 span:nth-child(13) {
		animation-delay: 0.7s;
	}
	h1 span:nth-child(14) {
		animation-delay: 0.8s;
	}

	/* ANIMATION */
	@keyframes bounce {
		100% {
			top: -330px;
			text-shadow:
				0 1px 0 #ccc,
				0 2px 0 #ccc,
				0 3px 0 #ccc,
				0 4px 0 #ccc,
				0 5px 0 #ccc,
				0 6px 0 #ccc,
				0 7px 0 #ccc,
				0 8px 0 #ccc,
				0 9px 0 #ccc,
				0 50px 25px rgba(0, 0, 0, 0.2);
		}
	}
</style>
