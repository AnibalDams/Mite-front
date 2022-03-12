<script>
	import NavBar from '../components/navbar.svelte';
	import PrevieAnimeInformation from '../components/previewAnimeInformation.svelte';
</script>

<div
	style="max-width: 100%;height: 600px;background-image: linear-gradient(to  top   ,rgb(13,13,13) ,transparent), linear-gradient(to  right,rgb(13,13,13) ,transparent 80%),url('https://mite-api.herokuapp.com/img/wonder_egg_priority_main.png');background-position: center;background-size: cover; "
>
	<NavBar />
	<PrevieAnimeInformation />
</div>
