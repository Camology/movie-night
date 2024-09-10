<script>
	import Counter from './Counter.svelte';
	import welcome from '$lib/images/svelte-welcome.webp';
	import welcome_fallback from '$lib/images/svelte-welcome.png';
	import Calendar from '@event-calendar/core';
    import TimeGrid from '@event-calendar/time-grid';

	let plugins = [TimeGrid];
    let options = {
        view: 'timeGridWeek',
        events: [
            // your list of events
        ]
    };

	let movie_title = "";
	let movie_info = "";
	
	function printHotdog() {
		console.log("hotdog");
	}

	function getMovieInfo() {
		let url = "http://www.omdbapi.com/?apikey=GETYOUROWNAPIBASTARD&t="
		url = url.concat(movie_title)
		fetch(url)
		.then((response) => response.json())
		// .then((json) => console.log(json))
		.then((json) => movie_info = JSON.stringify(json));

	}
</script>

<svelte:head>
	<title>Home</title>
	<meta name="description" content="Svelte demo app" />
</svelte:head>

<section>
	<label for="movie-input">MOVIE TITLE:</label>
	<input bind:value={movie_title} placeholder="enter your title" />
	<button on:click={getMovieInfo}>
		SUBMIT {movie_title}
	</button>

	<p>You submitted: {movie_title}</p>
	<p>I found... {movie_info}</p>

	<Calendar {plugins} {options} />


	<!-- <h1>
		<span class="welcome">
			<picture>
				<source srcset={welcome} type="image/webp" />
				<img src={welcome_fallback} alt="Welcome" />
			</picture>
		</span>

		to your new<br />SvelteKit app
	</h1>

	<h2>
		try editing <strong>src/routes/+page.svelte</strong>
	</h2>

	<Counter /> -->
</section>

<style>
	section {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		flex: 0.6;
	}

	h1 {
		width: 100%;
	}

	.welcome {
		display: block;
		position: relative;
		width: 100%;
		height: 0;
		padding: 0 0 calc(100% * 495 / 2048) 0;
	}

	.welcome img {
		position: absolute;
		width: 100%;
		height: 100%;
		top: 0;
		display: block;
	}
</style>
