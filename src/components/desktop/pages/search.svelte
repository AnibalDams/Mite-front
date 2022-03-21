<script type="text/javascript">
	import NavBar from '../components/navbar.svelte';
	import AnimeList from '../components/coverList.svelte';
	export let data;
	export let searchIndex;
</script>

<NavBar />

{#if data[0].message === 'No se encontro nungun anime.'}
	<span>No se encontro ningun anime.</span>
{:else}
	<div class="help-text">
		<span class="material-icons-round">search</span><span>Resultados de: {searchIndex}</span>
	</div>

	<AnimeList {data} />
{/if}

<style type="text/css">
	.help-text {
		display: flex;
		justify-content: flex-start;
		align-items: center;
		margin: 30px;
		font-size: 2rem;
		font-weight: 400;
	}
	.material-icons-round {
		font-weight: bold;

		margin-right: 10px;
	}
</style>
