<script>
	let time = new Date();
	setInterval(() => (time = new Date()), 1000);

    const getWeather = async () => (await fetch('https://api.open-meteo.com/v1/forecast?latitude=30.430324&longitude=-97.74324&current=temperature_2m,weather_code&hourly=temperature_2m,precipitation_probability,weather_code&daily=weather_code,temperature_2m_max,temperature_2m_min,precipitation_probability_max&temperature_unit=fahrenheit&wind_speed_unit=mph&precipitation_unit=inch&timezone=auto')).json();
    let weather = getWeather();
</script>

<main>
    <section id="clock">
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
    </section>
    <section id="weather">
        {#await weather}
            <p>Loading weather...</p>
        {:then data}
            <h1>{Math.round(data.current.temperature_2m)}</h1>
            {#each data.daily.time as day, index}
                <h2>
                    {new Date(day).toLocaleString('en-US', { weekday: 'short', timeZone: 'UTC' })}
                    {Math.round(data.daily.temperature_2m_max[index])}
                    {Math.round(data.daily.temperature_2m_min[index])}
                </h2>
            {/each}
        {:catch error}
            <p>{error}</p>
        {/await}
    </section>
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
        display: flex;
        justify-content: space-between;
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
		/* background: rgba(18, 16, 16, 0.1); */
        background: repeating-linear-gradient(0deg, color-mix(in srgb, rgba(49%, 98%, 72%) 100%, transparent) 0 1px, transparent 1px 50px),repeating-linear-gradient(90deg, color-mix(in srgb, rgba(49%, 98%, 72%) 100%, transparent) 0 1px, transparent 1px 50px);
		opacity: 1;
		z-index: -1;
		pointer-events: none;
		/* animation: flicker 0.15s infinite; */
	}
</style>
