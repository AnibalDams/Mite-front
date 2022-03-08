<script type="text/javascript">
	import { page } from '$app/stores';
	import { gql, operationStore, query } from '@urql/svelte';
	import AnimeList from '../../../components/mobileComponents/AnimeList.svelte';
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
	<div class="loading" />
{:else}
	<AnimeList data={$all} dataType="findAnimeByGenre" />
{/if}

<style type="text/css">
	.navBar {
		width: 100%;
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
	.loading {
		display: inline-block;
		margin-left: 50%;
		margin-top: 100px;
		padding: 20px;
		border: 1px solid #aaa;
		border-radius: 5px;
		animation: loading infinite 2s ease-in-out;
	}
	@keyframes loading {
		from {
			transform: rotate(0);
		}
		to {
			transform: rotate(360deg);
		}
	}
</style>
