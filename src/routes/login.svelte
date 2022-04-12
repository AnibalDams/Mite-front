<script type="text/javascript">
	import LoginMobile from '../components/mobileComponents/login.svelte';
	import LoginDesktop from '../components/desktop/pages/login.svelte';
	import { gql, operationStore, query } from '@urql/svelte';

	let width;
	const queryAnimes = gql`
		query {
			animeRandom {
				image
			}
		}
	`;
	const all = operationStore(queryAnimes);
	query(all);
</script>

<svelte:window bind:innerWidth={width} />

{#if $all.fetching != true}
	{#if width > 1020}
		<LoginDesktop image={$all.data.animeRandom.image} />
	{:else}
		<LoginMobile image={$all.data.animeRandom.image} />
	{/if}
{/if}
