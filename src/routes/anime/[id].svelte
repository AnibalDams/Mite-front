<script>
	import AnimeDetails from '../../components/mobileComponents/animeDetails.svelte';
	import AnimeDetailsD from '../../components/desktop/pages/animeDetails.svelte';
	import Loading from '../../components/mobileComponents/loading.svelte';
	import { page } from '$app/stores';

	import { gql, operationStore, query } from '@urql/svelte';
	let width;
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
				type
			}
			findEpisodes(animeID: $animeId) {
				anime
				episodeName
				message
				episodeNumber
				thumbnail
			}
		}
	`;
	const all = operationStore(queryAnimes, { animeId });
	query(all);
</script>

<svelte:window bind:innerWidth={width} />

<svelte:head>
	{#if $all.fetching}
		<title>Cargando...</title>
	{:else if $all.data['findAnime'].message === 'El anime solicitado no existe.'}
		<title>El anime solicitado no existe.</title>
	{:else}
		<meta name="description" content={`${$all.data['findAnime'].synopsis}`} />

		<meta
			name="keywords"
			content={`Anime, mite, Mite, ver anime, ver anime online, ver anime gratis en espanol, ver anime top, ver anime en espanol latino, ver anime gratis online, anime series, anime, ver ${$all.data['findAnime'].name},ver ${$all.data['findAnime'].name} subtitulado, ver ${$all.data['findAnime'].name} sub español, ${$all.data['findAnime'].name} de que se trata, ${$all.data['findAnime'].name} final, ${$all.data['findAnime'].name} episodios`}
		/>
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
{:else if width > 1020}
	<AnimeDetailsD anime={$all.data['findAnime']} episodes={$all.data['findEpisodes']} />
{:else}
	<AnimeDetails data={$all} />
{/if}
