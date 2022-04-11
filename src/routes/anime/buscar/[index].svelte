<script type="text/javascript">
	import SearchPage from '../../../components/desktop/pages/search.svelte';
	import Loading from '../../../components/mobileComponents/loading.svelte';
	import { gql, operationStore, query } from '@urql/svelte';

	import { page } from '$app/stores';

	let searchIndex = $page.params.index;

	const queryAnimes = gql`
		query ($searchIndex: String!) {
			search(anime: $searchIndex) {
				message
				id
				name
				cover
				releaseDate
				type
			}
		}
	`;
	const all = operationStore(queryAnimes, { searchIndex }, { requestPolicy: 'cache-first' });

	query(all);
</script>

<svelte:head>
	<title>Buscar - {searchIndex}</title>
	<link
		rel="alternate"
		media="only screen and (max-width: 1020px)"
		href="https://mite-jade.vercel.app/buscar"
	/>
</svelte:head>
{#if $all.fetching === false}
	<SearchPage {searchIndex} data={$all.data['search']} />
{:else}
	<Loading />
{/if}
