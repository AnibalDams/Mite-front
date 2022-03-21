<script type="text/javascript">
	import AnimeDetails from '../components/animeDetails.svelte';
	export let anime;
	export let episodes;
</script>

<main
	class="main"
	style="background-image: linear-gradient(to  top   ,rgb(13,13,13) ,transparent), linear-gradient(to  right,rgb(13,13,13) ,transparent 60%),linear-gradient(to  left,rgb(13,13,13) ,transparent 40%),url({anime.image});"
>
	<AnimeDetails {anime} {episodes} />
</main>

<style type="text/css">
	.main {
		max-width: 100%;
		height: 700px;
		background-position: center;
		background-size: cover;
	}
</style>
