<script>
	import { initClient } from '@urql/svelte';

	initClient({
		url: 'https://mite-api.herokuapp.com/graphql'
	});
</script>

<svelte:head>
	<meta name="author" content="Anibal Dams" />
	<meta name="robots" content="index,follow" />

	<meta
		name="keywords"
		content="Anime, mite, Mite, ver anime, ver anime online, ver anime gratis en espanol, ver anime top, ver anime en espanol latino, ver anime gratis online, anime series, anime"
	/>
</svelte:head>
<slot />
