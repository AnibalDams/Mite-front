<script>
	import { initClient } from '@urql/svelte';
	import DesktopNavbar from '../components/desktop/components/navbar.svelte';
	import Notifications from 'svelte-notifications';
	import { SvelteToast } from '@zerodevx/svelte-toast';

	initClient({
		url: 'https://mite-api.herokuapp.com/graphql'
	});
	let width;
</script>

<svelte:window bind:innerWidth={width} />
<SvelteToast />
<Notifications>
	<slot />
</Notifications>
