<script type="text/javascript">
	import { page } from '$app/stores';
	import { gql, operationStore, query } from '@urql/svelte';
	import AnimeList from '../../../components/mobileComponents/AnimeList.svelte';
	import GenrePageD from '../../../components/desktop/pages/genre.svelte'
	import Loading from '../../../components/mobileComponents/loading.svelte';
	let genre = $page.params.genero;
	let width;
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
	const all = operationStore(queryAnimes, { genre });
	query(all);
</script>
<svelte:window bind:innerWidth={width} />

<svelte:head>
	<title>Animes del genero {genre} - Mite</title>
</svelte:head>


{#if $all.fetching}
	<Loading />
{:else}
{#if width>1020}
<GenrePageD genreName={genre} animes={$all.data['findAnimeByGenre']}/>
{:else}

<h3 class="genre">{genre}</h3>
<nav class="navBar">
	<button on:click={() => window.history.back()}
		><span class="material-icons-round">arrow_back</span></button
	>
</nav>
	<AnimeList data={$all} dataType="findAnimeByGenre" />
{/if}
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
