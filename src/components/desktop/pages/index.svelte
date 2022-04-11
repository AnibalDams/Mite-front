<script>
	import NavBar from '../components/navbar.svelte';
	import PreviewAnimeInformation from '../components/previewAnimeInformation.svelte';
	import CoverList from '../components/coverList.svelte';
	import EpisodesSlider from '../components/episodesSlider.svelte';
	import { gql, operationStore, query } from '@urql/svelte';

	const queryAnimes = gql`
		query {
			latestAnimesAdded {
				message
				id
				name
				synopsis
				cover
				type
				releaseDate
			}
			latestEpisodesAdded {
				anime
				animeName
				thumbnail
				episodeNumber
			}
			mostPopularAnime {
				message
				id
				name
				synopsis
				cover
				type
				releaseDate
			}

			animeRandom {
				id
				name
				synopsis
				type
				study
				releaseDate
				image
			}
			findGenres {
				genre
			}
			animeAndGenreRandom {
				genre
				animes {
					message
					id
					name
					synopsis
					cover
					type
					releaseDate
				}
			}
		}
	`;
	const all = operationStore(queryAnimes);
	query(all);
</script>

{#if $all.fetching}
	<div />
{:else}
	{#if $all.fetching === false}
		<div
			style="max-width: 100%;height: 600px;background-image: linear-gradient(to  top   ,rgb(13,13,13) ,transparent), linear-gradient(to  right,rgb(13,13,13) ,transparent 60%),linear-gradient(to  left,rgb(13,13,13) ,transparent 40%),url({$all
				.data['animeRandom'].image});background-position: center;background-size: cover; "
		>
			<NavBar />
			<PreviewAnimeInformation animeData={$all.data['animeRandom']} />
		</div>
	{/if}
	<span class="text-big" style="margin-top:100px;">Ultimos episodios agregados</span>
	{#if $all.fetching === false}
		<EpisodesSlider episodeData={$all.data['latestEpisodesAdded']} />
	{/if}
	<span class="text-big" style="margin-top: 20px;">Ultimos Animes Agregados</span>
	{#if $all.fetching === false}
		<CoverList data={$all.data['latestAnimesAdded']} type="normal" />
	{/if}
	<span class="text-big" style="margin-top:100px;">Animes más populares</span>
	{#if $all.fetching === false}
		<CoverList data={$all.data['mostPopularAnime']} type="normal" />
	{/if}
	<span class="text-big" style="margin-top:100px;">{$all.data['animeAndGenreRandom'].genre}</span>
	<CoverList data={$all.data['animeAndGenreRandom'].animes} type="normal" />
{/if}

<style>
	.text-big {
		display: inline-block;
		font-size: 2rem;
		font-weight: bold;
		margin-left: 30px;
	}
</style>
