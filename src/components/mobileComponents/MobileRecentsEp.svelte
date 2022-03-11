<script>
	export let data = [];
</script>

<div class="scrollmenu">
	{#if data.length === 0}
		<div />
	{:else}
		{#each data as episode}
			<a href={`/anime/episodio/${episode.anime}/${episode.episodeNumber}`}>
				<div class="container">
					<img src={episode.thumbnail} alt="episode thumbnail" loading="lazy" />
					{#if episode.animeName && episode.animeName.length >= 25}
						<span>{episode.animeName.substring(0, 25)}... - {episode.episodeNumber}</span>
					{:else if episode.animeName === null}
						<span>... - {episode.episodeNumber}</span>
					{:else}
						<span>{episode.animeName} - {episode.episodeNumber}</span>
					{/if}
				</div>
			</a>
		{/each}
	{/if}
</div>

<style>
	div.scrollmenu {
		overflow: auto;
		white-space: nowrap;
		padding: 10px;
	}

	div.scrollmenu a {
		display: inline-block;

		color: white;
		text-align: center;

		text-decoration: none;
	}

	div.scrollmenu a div {
		display: flex;
		flex-direction: column;
		justify-content: flex-start;
		align-items: flex-start;
		margin-left: 10px;
		margin-right: 10px;
	}
	div.scrollmenu a img {
		width: 250px;
		height: 150px;
		object-fit: cover;
		border-radius: 5px;
	}
	div.scrollmenu a span {
		margin-top: 5px;
		font-size: 1rem;
		font-weight: 600;
	}

	div.scrollmenu a:hover {
		opacity: 0.5;
	}
</style>
