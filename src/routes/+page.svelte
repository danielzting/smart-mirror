<script>
	let time = new Date();

	setInterval(() => (time = new Date()), 1000);
</script>

<main>
	<h2>
		{time.toLocaleString('en-US', {
			year: 'numeric',
			month: 'long',
			day: 'numeric'
		})}
	</h2>
	<h1>
		{time.toLocaleString('en-US', {
			hour: 'numeric',
			minute: 'numeric',
			second: 'numeric'
		})}
	</h1>
</main>

<style>
	main {
		height: 100%;
		width: 100%;
		color: #ff8c28;
		border: 2px solid #ff8c28;
		font-family: 'Eva Matisse Classic';
		padding: 20px;
		filter: blur(0.5px);
		text-transform: uppercase;
		text-shadow: 0 0 1px white;
	}

	@font-face {
		font-family: 'Eva Matisse Classic';
		src: URL('/eva-matisse-classic.ttf') format('truetype');
	}

	h1 {
		font-size: 100pt;
		margin: 0;
	}

	h2 {
		font-size: 50pt;
		margin: 0;
	}

	h1,
	h2 {
		transform-origin: 0;
		transform: scaleX(0.6);
	}

	/* https://aleclownes.com/2017/02/01/crt-display.html */
	@keyframes flicker {
		0% {
			opacity: 0.27861;
		}
		5% {
			opacity: 0.34769;
		}
		10% {
			opacity: 0.23604;
		}
		15% {
			opacity: 0.90626;
		}
		20% {
			opacity: 0.18128;
		}
		25% {
			opacity: 0.83891;
		}
		30% {
			opacity: 0.65583;
		}
		35% {
			opacity: 0.67807;
		}
		40% {
			opacity: 0.26559;
		}
		45% {
			opacity: 0.84693;
		}
		50% {
			opacity: 0.96019;
		}
		55% {
			opacity: 0.08594;
		}
		60% {
			opacity: 0.20313;
		}
		65% {
			opacity: 0.71988;
		}
		70% {
			opacity: 0.53455;
		}
		75% {
			opacity: 0.37288;
		}
		80% {
			opacity: 0.71428;
		}
		85% {
			opacity: 0.70419;
		}
		90% {
			opacity: 0.7003;
		}
		95% {
			opacity: 0.36108;
		}
		100% {
			opacity: 0.24387;
		}
	}

	main::before {
		content: ' ';
		display: block;
		position: absolute;
		top: 0;
		left: 0;
		bottom: 0;
		right: 0;
		background: linear-gradient(rgba(18, 16, 16, 0) 50%, rgba(0, 0, 0, 0.25) 50%),
			linear-gradient(90deg, rgba(255, 0, 0, 0.06), rgba(0, 255, 0, 0.02), rgba(0, 0, 255, 0.06));
		z-index: 2;
		background-size:
			100% 2px,
			3px 100%;
		pointer-events: none;
	}

	main::after {
		content: ' ';
		display: block;
		position: absolute;
		top: 0;
		left: 0;
		bottom: 0;
		right: 0;
		background: rgba(18, 16, 16, 0.1);
		opacity: 0;
		z-index: 2;
		pointer-events: none;
		animation: flicker 0.15s infinite;
	}
</style>
