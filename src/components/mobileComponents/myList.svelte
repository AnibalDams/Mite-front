<script type="text/javascript">
	import { onMount } from 'svelte';

	import AnimeList from './AnimeList.svelte';
	import { gql, operationStore, query } from '@urql/svelte';
	import cookie from 'cookie-cutter';
	
	let profile = "n";
	

	const queryAnimes = gql`
		query ($profile: String!) {
			 findAnimesInList(userProfile:$profile){
				    message
				    _id
				    animeId
				    animeName
				    animeSynopsis
				    animeMain
				    animeCover
				    userProfile
				    createdAt
				    
  			}
  			 	selectUserProfile(id:$profile){
    				name
 				 }
		}
	`;
	const all = operationStore(queryAnimes, { profile }, { requestPolicy: 'cache-first' });
	query(all)


	onMount(() => {
		
		profile = cookie.get('profileName');

		$all.variables = { profile };

		all.reexecute({ requestPolicy: 'network-only' });
	});

</script>


<svelte:head>
	<title>Lista de {profile === null || profile === undefined || profile === 'null'? "Nadie":$all.fetching === false?$all.data.selectUserProfile.name:"cargando"} - AnimeMite</title>
</svelte:head>


{#if profile !== null || profile !== undefined || profile !== 'null'}
	<h3 class="text">Mi lista</h3>
	<nav class="navBar">
		<button on:click={() => window.history.back()}
			><span class="material-icons-round">arrow_back</span></button
		>
	</nav>
	
<section class="result">
		{#if $all.fetching === false}

		{#each $all.data.findAnimesInList as anime}
			
				<a href={`/anime/${anime.animeId}`} class="item">
					<img class="cover" loading="lazy" alt={anime.animeName} src={anime.animeCover} />
					{#if anime.animeName.length >= 25}
						<span class="title">
							{anime.animeName.substring(0, 25)}...
						</span>
					{:else}
						<span class="title">{anime.animeName}</span>
					{/if}
				</a>
			
		{/each}
	

		{/if}
</section>
{:else}
<a href="/" class="text-big" style="font-size: 2rem;font-weight: bold; display: block; text-align: center;  margin-top:300px; text-decoration: none;">Volver al inicio</a>


{/if}




<style type="text/css">
	.navBar {
		max-width: 100%;
		height: 30px;
		margin: 10px;
	}
	.navBar button {
		cursor: pointer;
		font-size: 1.2rem;
		background: none;
		border: none;
	}
	.text {
		margin: 10px;
		font-size: 1.5rem;
	}

		
	.result {
		display: flex;
		flex-direction: row;
		flex-wrap: wrap;
		height: fit-content;
		max-width: 100%;
		justify-content: center;
		margin-top: 20px;
	}
	.item {
		display: flex;
		flex-direction: column;

		margin-top: 5px;
		margin-bottom: 15px;
		width: 150px;
		text-decoration: none;
		text-transform: capitalize;
	}
	.item:hover {
		opacity: 0.5;
	}
	.cover {
		width: 100px;
		height: 158px;
		border-radius: 5px;
		object-fit: cover;
	}
	.title {
		margin-top: 10px;
		font-size: 18px;
	}
	span.releaseText {
		font-weight: 300;
		font-size: 15px;
	}
	.icon-button {
		margin-right: 20px;
		font-size: 1.2rem;
	}
	.icon-button:active {
		opacity: 0.5;
	}

</style>
