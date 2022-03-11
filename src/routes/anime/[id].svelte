<script>
	import AnimeDetails from '../../components/mobileComponents/animeDetails.svelte';
	import Loading from '../../components/mobileComponents/loading.svelte';
	import { page } from '$app/stores';

	import { gql, operationStore, query } from '@urql/svelte';

	let animeId = $page.params.id;
	const queryAnimes = gql`
		query ($animeId: String!) {
			findAnime(animeID: $animeId) {
				message
				id
				name
				synopsis
				image
				cover
				genres
				releaseDate
				onGoing
				study
			}
			findEpisodes(animeID: $animeId) {
				message
				episodeNumber
				thumbnail
			}
		}
	`;
	const all = operationStore(queryAnimes, { animeId });
	query(all);
</script>

<svelte:head>
	{#if $all.fetching}
		<title>Cargando...</title>
	{:else if $all.data['findAnime'].message === 'El anime solicitado no existe.'}
		<title>El anime solicitado no existe.</title>
	{:else}
		<title>Ver {$all.data['findAnime'].name} - Mite</title>
	{/if}
</svelte:head>

{#if $all.fetching}
	<Loading />
{:else if $all.data['findAnime'].message === 'El anime solicitado no existe.'}
	<div style="width:100%; display: flex; justify-content:center;align-items: center;">
		<span
			style="display: inline-block;margin-top: 270px;margin-left: 10px;margin-right: 10px;font-size: 1.2rem;font-weight: bold;"
			>El anime solicitado no existe <a href="/">Vuelve al inicio</a></span
		>
	</div>
{:else}
	<AnimeDetails data={$all} />
{/if}
