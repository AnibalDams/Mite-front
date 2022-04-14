<script>
	import { createClient, setClient } from '@urql/svelte';

	import DesktopNavbar from '../components/desktop/components/navbar.svelte';
	import Notifications from 'svelte-notifications';
	import { SvelteToast } from '@zerodevx/svelte-toast';

	const client = createClient({
		url: 'https://mite-api.herokuapp.com/graphql'
	});

	setClient(client);
	let width;
</script>

<svelte:window bind:innerWidth={width} />
<SvelteToast />
<Notifications>
	<slot />
</Notifications>
