<script type="text/javascript">
	import NavBar from '../components/navbar.svelte';
	import AnimeList from '../components/coverList.svelte';
	export let genreName;
	export let animes;
</script>

<NavBar />

<h3 style="font-size:3rem; margin: 30px;">{genreName}</h3>
<AnimeList data={animes} type="normal" />
