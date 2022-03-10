<script>
	import AnimeDetails from '../../components/mobileComponents/animeDetails.svelte';
	import { page } from '$app/stores';

	import { gql, operationStore, query } from '@urql/svelte';

	let animeId = $page.params.id;
	const queryAnimes = gql`
		query{
			  
			  findAnime(animeID:${animeId}){
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
			  findEpisodes(animeID:${animeId}){
			    message
			    episodeNumber
			    thumbnail
			  }
		}
	`;
	const all = operationStore(queryAnimes);
	query(all);
	// console.log($all)
</script>

<svelte:head>
	{#if $all.fetching}
		<title>Cargando...</title>
	{:else if $all.data['findAnime'].message === 'El anime solicitado no existe.'}
		<title>El anime solicitado no existe.</title>
	{:else}
		<title>ver {$all.data['findAnime'].name} - Mite</title>
	{/if}
</svelte:head>

{#if $all.fetching}
	<span
		style="display: inline-block;text-align: center;margin-top: 270px;margin-left:10px;font-size: 1.2rem;font-weight: bold;"
		>Cargando...</span
	>
{:else if $all.data['findAnime'].message === 'El anime solicitado no existe.'}
	<span
		style="display: inline-block;margin-top: 270px;margin-left:10px;font-size: 1.2rem;font-weight: bold;"
		>El anime solicitado no existe <a href="/">Vuelve al inicio</a></span
	>
{:else}
	<AnimeDetails data={$all} />
{/if}
