<script>
	import MainContent from './mainContent.svelte';

	export let data;
</script>

<MainContent dataAnime={$data.data['findAnime']} dataEpisodes={$data.data['findEpisodes']} />
