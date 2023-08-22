<script>
	import Timer from './Timer.svelte';
	import { onMount } from 'svelte';

	let gifIndex = Math.floor(Math.random() * 12) + 1;
	let gifURL = `/gifs/Gif_${gifIndex}.gif`;

	onMount(() => {
		setInterval(() => {
			gifIndex = Math.floor(Math.random() * 12) + 1;
			gifURL = `/gifs/Gif_${gifIndex}.gif`;
		}, 40000); // 40sec 40000

		setInterval(() => {
			gifIndex = Math.floor(Math.random() * 12) + 1;
			gifURL = `/gifs/Gif_${gifIndex}.gif`;
		}, 110000); //1:50min 110000
	});

</script>

<svelte:head>
	<link rel="stylesheet" href="node_modules/bootstrap/dist/css/bootstrap.min.css">
</svelte:head>

<div class="video-background" style="background-image: url({gifURL});"></div>

<main>
	<h1 class="text-center mb-4">Pomodoro Lofi Timer</h1>
	<Timer />
</main>
