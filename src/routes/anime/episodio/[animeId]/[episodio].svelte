<script type="text/javascript">
	import EpisodesList from '../../../../components/mobileComponents/episodeList.svelte';
	import EpisodeD from '../../../../components/desktop/pages/episode.svelte';

	import { gql, operationStore, query } from '@urql/svelte';
	import { page } from '$app/stores';
	let haveEpisode;
	let height;
	let animeId = $page.params.animeId;
	let episodeNumber = Number($page.params.episodio) - 1;
	$: episodeParam = Number($page.params.episodio);
	$: if (episodeParam) {
		episodeNumber = episodeParam - 1;
	}
	let urls = [];
	let width;
	const queryAnimes = gql`
		query ($animeId: String!) {
			animeRandom {
				image
			}
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
				message
				anime
				episodeNumber
				episodeName
				thumbnail
				servers {
					url
				}
			}
		}
	`;

	const all = operationStore(queryAnimes, { animeId });

	query(all);
	$: if (
		!$all.fetching &&
		$all.data['findEpisodes'][0].message === 'Este anime no cuenta con ningun episodio aun.'
	) {
		haveEpisode = false;
	} else {
		haveEpisode = true;
	}

	$: if (
		$all.fetching === false &&
		$all.data['findAnime'].message != 'El anime solicitado no existe.' &&
		$all.data['findEpisodes'][0].message != 'Este anime no cuenta con ningun episodio aun.'
	) {
		$all.data['findEpisodes'].forEach((el) => {
			urls = [...urls, el.servers[0].url];
		});
	}
</script>

<svelte:window bind:innerHeight={height} bind:innerWidth={width} />

<svelte:head>
	{#if !$all.fetching}
		<meta
			name="description"
			content={`Ver ${$all.data['findAnime'].name} Sub Español, descargar ${$all.data['findAnime'].name} gratis, ${$all.data['findAnime'].name} en calidad HD.`}
		/>
		<meta property="og:title" content={`${$all.data['findAnime'].name}`} />
		<meta
			property="og:url"
			content={`/anime/episodio/${$all.data['findAnime'].id}/${episodeParam}`}
		/>
		<meta
			property="og:description"
			content={`Estoy viendo ${$all.data['findAnime'].name} Completo en Calidad HD, completamente Gratis!`}
		/>
		<link
			rel="canonical"
			href={`https://mite-jade.vercel.app/anime/episodio/${$all.data['findAnime'].id}/${episodeParam}`}
		/>
		{#if $all.data['findAnime'].message === 'El anime solicitado no existe.'}
			<title>El anime solicitado no existe</title>
		{:else}
			<title>{$all.data['findAnime'].name} Episodio {episodeParam} Sub Español - Mite</title>
		{/if}
	{:else}
		<title>Cargando...</title>
	{/if}
</svelte:head>

{#if $all.fetching}
	<div />
{:else if !$all.fetching && $all.data['findAnime'].message === 'El anime solicitado no existe.'}
	<div
		style="width:100%; height: 100%;background-image: linear-gradient(to  top   ,rgb(13,13,13) ,transparent), linear-gradient(to  right,rgb(13,13,13) ,transparent 60%),linear-gradient(to  left,rgb(13,13,13) ,transparent 40%),url({$all
			.data['animeRandom']
			.image});background-position: top;background-size: cover; display: flex; justify-content:center;align-items: center;"
	>
		<span
			style="display: inline-block;margin-top: 270px;margin-left: 10px;height: 300px;margin-right: 10px;font-size: 1.2rem;font-weight: bold;"
			>El anime solicitado no existe <a href="/" style="text-decoration: underline;"
				>Vuelve al inicio</a
			></span
		>
	</div>
{:else if !haveEpisode}
	<div
		style="width:100%; height: 100%;background-image: linear-gradient(to  top   ,rgb(13,13,13) ,transparent), linear-gradient(to  right,rgb(13,13,13) ,transparent 60%),linear-gradient(to  left,rgb(13,13,13) ,transparent 40%),url({$all
			.data['findAnime']
			.image});background-position: top;background-size: cover; display: flex; justify-content:center;align-items: center;"
	>
		<span
			style="display: inline-block;margin-top: 270px;margin-left: 10px;height: 300px;margin-right: 10px;font-size: 1.2rem;font-weight: bold;"
			>{$all.data['findAnime'].name} no cuenta con ningun episodio, aun.
			<a on:click={() => window.history.back()} style="text-decoration: underline;">Volver.</a
			></span
		>
	</div>
{:else if width > 1020}
	<EpisodeD
		{urls}
		{episodeNumber}
		{episodeParam}
		anime={$all.data['findAnime']}
		episodes={$all.data['findEpisodes']}
	/>
{:else}
	<main>
		<nav class="navBar">
			<a href={`/anime/${$page.params.animeId}`} style="display: flex; align-items: center;">
				{#if $all.data['findAnime'].name.length > 25}
					<span class="material-icons-round">arrow_back</span><span class="title"
						>{$all.data['findAnime'].name.substring(0, 25)}... - {episodeNumber + 1}</span
					>
				{:else}
					<span class="material-icons-round">arrow_back</span><span class="title"
						>{$all.data['findAnime'].name.substring(0, 25)} - {episodeNumber + 1}</span
					>
				{/if}
			</a>
			<a href="/"><span class="material-icons-round">share</span></a>
		</nav>
		{#if urls.length > 0}
			<iframe
				src={urls[episodeNumber]}
				class="video"
				scrolling="no"
				frameborder="0"
				allowfullscreen
			/>
		{:else}
			<div class="video" />
		{/if}
		<div class="action">
			{#if Number($page.params.episodio) > 1}
				<a
					on:click={() => {
						episodeNumber = episodeNumber - 1;
					}}
					href={`/anime/episodio/${$page.params.animeId}/${Number($page.params.episodio) - 1}`}
					class="button"><span class="material-icons-round">chevron_left</span></a
				>
			{:else}
				<div style="padding:15px;" />
			{/if}
			<a href={`/anime/${$page.params.animeId}`} class="button all"
				><span class="material-icons-round"> menu </span></a
			>
			{#if $all.data['findEpisodes'].length === Number($page.params.episodio)}
				<div style="padding:15px;" />
			{:else}
				<a
					on:click={() => {
						episodeNumber = episodeNumber + 1;
					}}
					href={`/anime/episodio/${$page.params.animeId}/${Number($page.params.episodio) + 1}`}
					class="button"><span class="material-icons-round">navigate_next</span></a
				>
			{/if}
		</div>

		<span class="moreText">Episodios de {$all.data['findAnime'].name}</span>
		<EpisodesList data={$all.data['findEpisodes']} animeId={$all.data['findAnime'].id} />
	</main>
{/if}

<style>
	main {
		overflow-x: hidden;
	}
	.title {
		margin-left: 10px;
		font-size: 1.1rem;
		font-weight: 500;
	}

	.navBar {
		background-color: transparent;
		width: 100%;
		height: 50px;
		display: flex;
		align-items: center;
		justify-content: space-between;
	}
	.action {
		display: flex;
		justify-content: space-between;
		align-items: center;
		margin: 10px;
	}
	.button {
		padding-top: 8px;
		padding-bottom: 5px;
		padding-left: 15px;
		padding-right: 15px;
		background-color: #1f1f1f;
		border-radius: 5px;
	}
	.button:hover {
		opacity: 0.5;
	}
	.button.all {
		background-color: #3f3f3f;
	}

	a {
		padding: 15px;
		cursor: pointer;
		text-decoration: none;
	}
	.material-icons-round {
		color: #eee;
		font-size: 1.4rem;
	}
	.video {
		width: 100%;
		margin-top: 50px;

		height: 400px;
	}
	.moreText {
		display: inline-block;
		margin-top: 40px;
		margin-left: 10px;
		margin-right: 10px;
		font-size: 1.2rem;
		font-weight: 600;
	}
</style>
