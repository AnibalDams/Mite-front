<script type="text/javascript">
	import { gql, operationStore, query, mutation } from '@urql/svelte';
	import cookie from 'cookie-cutter';

	export let anime;
	export let animeData;
	let loading = false;
	let profile = cookie.get('profileName');
	const addAnime = mutation({
		query: `
      		mutation ($animeId: String!, $animeName: String!, $animeSynopsis:String!,$animeMain:String!,$animeCover:String!,$userProfile:String!) {
			    addAnimeToList(animeId:$animeId,animeName:$animeName,animeSynopsis:$animeSynopsis,animeMain:$animeMain,animeCover:$animeCover,userProfile:$userProfile)


		}
    `
	});
	const deleteAnime = mutation({
		query: `
      		mutation ($animeId: String!) {
			    deleteAnimeInList(animeId:$animeId,secretKey:"anibalDams")


		}
    `
	});

	const queryAnimes = gql`
		query ($animeId: String!, $userProfile: String!) {
			findAnimeInList(animeId: $animeId, userProfile: $userProfile) {
				_id
				animeId
			}
		}
	`;
	const all = operationStore(queryAnimes, { animeId: anime, userProfile: profile });
	query(all);

	let addOrDeleteAnimeInList = async function () {
		if ($all.data.findAnimeInList.animeId === null) {
			loading = true;
			await addAnime({
				animeId: animeData.id,
				animeName: animeData.name,
				animeSynopsis: animeData.synopsis,
				animeMain: animeData.image,
				animeCover: animeData.cover,
				userProfile: profile
			});

			$all.variables = { animeId: anime, userProfile: profile };

			all.reexecute({ requestPolicy: 'network-only' });

			loading = false;
		} else {
			loading = true;
			await deleteAnime({ animeId: $all.data.findAnimeInList._id });

			$all.variables = { animeId: anime, userProfile: profile };
			all.reexecute({ requestPolicy: 'network-only' });
			loading = false;
		}
	};
</script>

<div class="container">
	{#if profile !== null || profile !== undefined || profile !== 'null'}
		<button class="button" on:click={addOrDeleteAnimeInList}>
			<span class="material-icons-round icon" style="color:#bbb;">add</span>
			<span style="color:#bbb;"
				>{loading || $all.fetching
					? 'Cargando...'
					: $all.fetching === false && $all.data.findAnimeInList.animeId === null
					? 'Agregar a mi lista'
					: 'Remover de mi lista'}</span
			>
		</button>
	{/if}
</div>

<style type="text/css">
	* {
	}
	.icon {
		margin-bottom: 5px;
	}
	.container {
		margin-top: 20px;
		width: 100%;
		display: flex;
		align-items: center;
		justify-content: center;
	}
	button.button:active {
		border-radius: 5px;
		background-color: rgba(187, 187, 187, 0.2);
	}
	button.button {
		cursor: pointer;
		background: none;
		padding: 5px;
		border: none;
		outline: none;
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		margin-right: 15px;
		font-weight: bold;
	}
</style>
