<script type="text/javascript">
	import { onMount } from 'svelte';
	import NavBar from '../components/navbar.svelte' 
	import PreviewAnimeInformationMinified from '../components/previewAnimeInformationMinified.svelte'
	import AnimeList from '../components/coverListMinified.svelte'
	import { gql, operationStore, query } from '@urql/svelte';
	import cookie from 'cookie-cutter';
	

	let profile = "n";
	let animeR = {animeName:"",animeSynopsis:"",animeId:""};
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
	let numeroR = 0
	$: if(!$all.fetching){
		if($all.data.findAnimesInList && $all.data.findAnimesInList.length >0){
		numeroR = Math.floor(Math.random() * ($all.data.findAnimesInList.length - 0 * 1) + 0)
		animeR =$all.data.findAnimesInList[numeroR]

		}
	}
	
	onMount(() => {
		
		profile = cookie.get('profileName');

		$all.variables = { profile };

		all.reexecute({ requestPolicy: 'network-only' });
	});

	query(all);

</script>

<svelte:head>
	<title>Lista de {profile === null || profile === undefined || profile === 'null'? "Nadie":$all.fetching === false?$all.data.selectUserProfile.name:"cargando"} - AnimeMite</title>
</svelte:head>

{#if profile === null || profile === undefined || profile === 'null'}
<a href="/" class="text-big" style="display: block; text-align: center;  margin-top:300px; text-decoration: none;">Volver al inicio</a>

{:else}
{#if $all.fetching != true}
	{#if $all.data.findAnimesInList.length ===0}
	<span style="display: block;text-align: center; margin-top: 300px; font-size: 2rem;font-weight: bold;">Aun no has agregado ningun anime a tu lista. <a href="/">Vuelve al inicio</a></span>
		{:else}
			<main style="max-width: 100%;height: 700px;background-image: linear-gradient(to  top   ,rgb(13,13,13) ,transparent), linear-gradient(to  right,rgb(13,13,13) ,transparent 60%),linear-gradient(to  left,rgb(13,13,13) ,transparent 40%),url({$all.data.findAnimesInList[numeroR].animeMain});background-position: center;background-size: cover; "
>
	<NavBar/>
	<PreviewAnimeInformationMinified animeData={animeR}/>
<span class="text-big" style="margin-top: 100px;display: flex; align-items: center;"><span class="material-icons-round" style="margin-right: 10px;">list</span>  Mi lista</span>
<AnimeList data={$all.data.findAnimesInList}/>
</main>

	{/if}
{/if}

{/if}




<style type="text/css">
	.text-big{
		display: inline-block;
		font-size: 2rem;
		margin-left: 40px;
		font-weight: bold;
	}
</style>