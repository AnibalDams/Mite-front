<script>
	import HomePageMobile from '../components/mobileComponents/homePageMobile.svelte';
	import HomePageDesktop from '../components/desktop/pages/index.svelte';

	let width;
</script>

<svelte:head>
	<meta
		name="description"
		content="Mite, una plataforma para ver anime online en HD subtitulado al español y leer manga (aun no implementado)"
	/>

	<meta
		name="keywords"
		content="Anime, mite, Mite, ver anime, ver anime online, ver anime gratis en espanol, ver anime top, ver anime en espanol latino, ver anime gratis online, anime series, anime"
	/>
</svelte:head>

<svelte:window bind:innerWidth={width} />

{#if width > 912}
	<HomePageDesktop />
{:else}
	<HomePageMobile />
{/if}

<style>
</style>
