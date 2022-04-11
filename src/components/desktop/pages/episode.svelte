<script type="text/javascript">
	let width = 2;
	import NavBar from '../components/navbar.svelte';
	import AnimeDetails from '../components/animeDetails.svelte';
	export let urls;
	export let animeId;
	export let episodeNumber;
	export let episodeParam;
	export let anime;
	export let episodes;
</script>

<svelte:window bind:innerWidth={width} />

<main
	class="main"
	style="background-image: linear-gradient(to  top   ,rgb(13,13,13) ,transparent), linear-gradient(to  right,rgb(13,13,13) ,transparent 60%),linear-gradient(to  left,rgb(13,13,13) ,transparent 40%),url({anime.image});"
>
	<NavBar />
	{#if urls.length > 0}
		<h1 style="margin-left:50px;font-size: 3.5rem;margin-top: 20px">
			{anime.name} episodio {episodeParam}
		</h1>

		<iframe
			src={urls[episodeNumber]}
			class="video"
			scrolling="no"
			frameborder="0"
			allowfullscreen
			style="margin-left: 50px;"
		/>
	{:else}
		<div class="video" />
	{/if}
</main>
<div style="margin-top:50px;">
	<AnimeDetails {anime} {episodes} />
</div>

<style type="text/css">
	.main {
		width: 100%;
		height: 800px;
		display: flex;
		flex-direction: column;
		justify-content: center;
		background-size: cover;
		background-position: center;
	}
	.video {
		background-color: #000;
		height: 550px;
		margin-top: 50px;
		margin-bottom: 50px;

		width: 950px;
	}
</style>
