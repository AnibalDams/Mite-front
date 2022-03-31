<script type="text/javascript">
	import AnimeDetails from '../components/animeDetails.svelte';
	import NavBar from '../components/navbar.svelte';
	import AnimeList from '../components/coverList.svelte'
	export let anime;
	export let episodes;
	import { gql, operationStore, query } from '@urql/svelte';
	const queryAnimes = gql`
		query ($genre: String!) {
			findAnimeByGenre(genre: $genre) {
				message
				id
				name
				cover
				releaseDate
				type
				synopsis
			}
		}
	`;
	const all = operationStore(queryAnimes, { genre:anime.genres[0] });
	query(all);
</script>
{#if $all.fetching===false}

<main
	class="main"
	style="background-image: linear-gradient(to  top   ,rgb(13,13,13) ,transparent), linear-gradient(to  right,rgb(13,13,13) ,transparent 60%),linear-gradient(to  left,rgb(13,13,13) ,transparent 40%),url({anime.image});">
	<NavBar />
	<AnimeDetails {anime} {episodes} />
	<p style="margin:30px;font-size: 2rem;font-weight: bold;">Relacionados</p>
	<AnimeList data={$all.data['findAnimeByGenre']} detail={true}/>

</main>

{/if}

<style type="text/css">
	.main {
		max-width: 100%;
		height: 700px;
		background-position: center;
		background-size: cover;
	}
</style>
