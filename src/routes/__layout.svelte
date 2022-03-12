<script>
	import { initClient } from '@urql/svelte';
	import DesktopNavbar from '../components/desktop/components/navbar.svelte'
	initClient({
		url: 'https://mite-api.herokuapp.com/graphql'
	});
	let width;

</script>



<svelte:window bind:innerWidth={width}/>

	<slot />




	