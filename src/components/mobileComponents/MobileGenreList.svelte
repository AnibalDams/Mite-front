<script>
	export let genres = [];
	genres.sort();
</script>

<div class="scrollmenu">
	{#each genres as genre}
		<a href={`/anime/genero/${genre}`}>{genre}</a>
	{/each}
</div>

<style>
	div.scrollmenu {
		overflow: auto;
		white-space: nowrap;
		padding: 10px;
	}

	div.scrollmenu a {
		display: inline-block;
		padding-top: 5px;
		padding-bottom: 5px;
		font-weight: 300;

		padding-left: 8px;
		padding-right: 8px;
		background: rgb(33, 33, 33);
		margin-right: 5px;
		border-radius: 8px;
		color: white;
		text-align: center;

		text-decoration: none;
	}

	div.scrollmenu a:hover {
		opacity: 0.5;
	}
</style>
