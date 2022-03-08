<script>
	import { initClient } from '@urql/svelte';

	initClient({
		url: 'https://mite-api.herokuapp.com/graphql'
	});
</script>

<slot />
