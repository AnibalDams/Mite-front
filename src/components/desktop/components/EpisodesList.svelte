<script type="text/javascript">
	export let episodes;
	console.log(episodes)
</script>

<div class="list">
	{#if episodes[0].message !="Este anime no cuenta con ningun episodio aun."}
		{#each episodes as episode}
			<a href={`/anime/episodio/${episode.anime}/${episode.episodeNumber}`} class="item">
				<img src={episode.thumbnail} class="thumbnail" />
				<span class="episodeDescription"
					>Episodio: {episode.episodeNumber} - {episode.episodeName}</span
				>
			</a>
		{/each}
	{:else}
		<span
			style="display: inline-block;width: 100%;margin-top: 40px;margin-right: 10px;font-size: 1.2rem;font-weight: bold;"
			>Aun no hay ningun episodio subido.</span
		>
	{/if}
</div>

<style type="text/css">
	.list {
		margin-top: 30px;
		margin-bottom: 30px;
		max-width: 100%;
		--auto-grid-min-size: 16rem;
		display: grid;
		grid-template-columns: repeat(auto-fill, minmax(var(--auto-grid-min-size), 1fr));
		grid-gap: 3rem;
	}

	.item {
		transition: 0.2;
		text-decoration: none;
		cursor: pointer;
		position: relative;
	}

	.item .thumbnail {
		width: 300px;
		height: 200px;
		object-fit: cover;
	}
	.item .episodeDescription {
		display: inline-block;
		font-weight: 300;
		margin-top: 10px;
		font-size: 1.1rem;
	}
</style>
