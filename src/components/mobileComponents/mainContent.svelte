<script>
	import NavBar from './navBarDetails.svelte';
	import EpisodesList from './episodeList.svelte';
	import Info from './info.svelte';

	export let dataAnime;
	export let dataEpisodes;
</script>

<div
	style=" height: 400px;background-image: linear-gradient(to top,rgb(13,13,13) 30%,transparent  ),url({dataAnime.image}); background-position: center;background-size: cover;"
>
	<NavBar />
	<Info data={dataAnime} />
	<EpisodesList data={dataEpisodes} animeId={dataAnime.id} />
</div>
