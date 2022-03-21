<script type="text/javascript">
	export let episodes;
</script>



<div class="list">
	{#each episodes as episode}

		<a href={`/anime/episodio/${episode.anime}/${episode.episodeNumber}`} class="item">
		<img src={episode.thumbnail} class="thumbnail" />
		<span class="episodeDescription">Episodio: {episode.episodeNumber} - {episode.episodeName}</span>
	</a>

	{/each}
</div>



<style type="text/css">
	.list{
		margin-top: 30px;
		margin-bottom: 30px;
		max-width: 100%;
		--auto-grid-min-size: 16rem;
		display: grid;
		grid-template-columns: repeat(auto-fill, minmax(var(--auto-grid-min-size), 1fr));
		grid-gap: 3rem;
		
	}
	
	.item{
		transition: 0.2;
		text-decoration: none;
		cursor: pointer;
		position: relative;
	}
	
	.item .thumbnail{
		width: 300px;
		height: 200px;
		object-fit: cover;
	}
	.item .episodeDescription{
		display: inline-block;
		font-weight: 300;
		margin-top: 10px;
		font-size: 1.1rem;
	}
</style>