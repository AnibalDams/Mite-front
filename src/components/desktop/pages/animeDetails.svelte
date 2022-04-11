<script type="text/javascript">
	import AnimeDetails from '../components/animeDetails.svelte';
	import NavBar from '../components/navbar.svelte';
	import AnimeList from '../components/coverList.svelte'
	export let anime;
	export let episodes;
	let genres = anime.genres.sort()
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
	const all = operationStore(queryAnimes, { genre:genres[0] });
	query(all);
	
</script>
{#if $all.fetching===false}

<main
	class="main"
	style="background-image: linear-gradient(to  top   ,rgb(13,13,13) ,transparent), linear-gradient(to  right,rgb(13,13,13) ,transparent 60%),linear-gradient(to  left,rgb(13,13,13) ,transparent 40%),url({anime.image});">
	<NavBar />
	<AnimeDetails {anime} {episodes} />

<p style="margin:30px;font-size: 2rem;font-weight: bold;">Tambien podria gustarte</p>
	
	<AnimeList data={$all.data['findAnimeByGenre'].sort(function (a, b) {

  if (a.name > b.name) {
    return 1;
  }
  if (a.name < b.name) {
    return -1;
  }
  // a must be equal to b
  return 0;
}

)} animeToFilter={anime.name} detail={true} type="recomendation"/>

	
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
