<script type="text/javascript">
	import { page } from '$app/stores';
	import { gql, operationStore, query } from '@urql/svelte';
	import AnimeList from '../../../components/mobileComponents/AnimeList.svelte';
	import Loading from '../../../components/mobileComponents/loading.svelte';
	let genre = $page.params.genero;

	const queryAnimes = gql`
		query ($genre: String!) {
			findAnimeByGenre(genre: $genre) {
				message
				id
				name
				cover
				releaseDate
			}
		}
	`;
	const all = operationStore(queryAnimes, { genre });
	query(all);
</script>

<svelte:head>
	<title>Animes del genero {genre} - Mite</title>
</svelte:head>

<nav class="navBar">
	<button on:click={() => window.history.back()}
		><span class="material-icons-round">arrow_back</span></button
	>
</nav>

<h3 class="genre">{genre}</h3>

{#if $all.fetching}
	<Loading />
{:else}
	<AnimeList data={$all} dataType="findAnimeByGenre" />
{/if}

<style type="text/css">
	.navBar {
		max-width: 100%;
		height: 30px;
		margin: 20px;
	}
	.navBar button {
		cursor: pointer;
		font-size: 1.2rem;
		background: none;
		border: none;
	}
	.genre {
		margin: 20px;
		font-size: 1.5rem;
	}
</style>
