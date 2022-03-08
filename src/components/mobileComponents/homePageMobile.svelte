<script>
	import MobileNavBar from './MobileNavBar.svelte';
	import MobileGenreList from './MobileGenreList.svelte';
	import MobileRecentsEps from './MobileRecentsEp.svelte';
	import MobileAnimeCoverList from './MobileAnimesCoverList.svelte';
	import MobilePopularAnimeList from './MobilePopularAnimeList.svelte';
	import { gql, operationStore, query } from '@urql/svelte';

	let genres = [];
	let eps = [];
	const queryAnimes = gql`
		query {
			latestAnimesAdded {
				message
				id
				name
				synopsis
				cover
			}
			latestEpisodesAdded {
				anime
				thumbnail
				episodeNumber
			}
			mostPopularAnime {
				message
				id
				name
				synopsis
				cover
				genres
			}
			findGenres {
				genre
			}
		}
	`;
	const all = operationStore(queryAnimes);
	query(all);
	$: if (!$all.fetching) {
		all.data['findGenres'].forEach((el) => (genres = [...genres, el.genre]));
		eps = all.data['latestEpisodesAdded'];
	}
</script>

<svelte:head>
	<title>Mite - Anime online en HD y con subtítulos en español</title>
</svelte:head>
{#if $all.fetching}
	<div class="loading" />
{:else}
	<MobileNavBar />
	<MobileGenreList {genres} />
	<span style="display: inline-block;margin:10px;color: #ddd; font-size: 1.2rem;font-weight: bold;"
		>Ultimos episodios agregados</span
	>
	<MobileRecentsEps data={eps} />

	<span style="display: inline-block;margin:10px;color: #ddd;  font-size: 1.2rem;font-weight: bold;"
		>Ultimos animes agregados</span
	>
	<MobileAnimeCoverList data={$all} dataName="latestAnimesAdded" />

	<span style="display: inline-block;margin:10px;color: #ddd;  font-size: 1.2rem;font-weight: bold;"
		>Animes Más visitados</span
	>
	<MobilePopularAnimeList data={$all} />
	{#if !$all.fetching}
		<footer
			style="width: 100%;height: 100px; display: flex; align-items:center;justify-content: center;border-top: 1px solid #aaa;"
		>
			<span style="font-weight: bold;"
				>Ningún vídeo se encuentra alojado en nuestros servidores. - <a
					href="https://github.com/anibalDams"
					target="_blank">Anibal Dams</a
				></span
			>
		</footer>
	{/if}
{/if}

<style>
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
