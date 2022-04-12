<script type="text/javascript">
	import SignUpMobile from '../components/mobileComponents/signUp.svelte';
	import SignUpDesktop from '../components/desktop/pages/signUp.svelte';
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
		<SignUpDesktop image={$all.data.animeRandom.image} />
	{:else}
		<SignUpMobile image={$all.data.animeRandom.image} />
	{/if}
{/if}
