<script type="text/javascript">
	export let data;
	export let animeId;
</script>

{#if data[0].message === 'Este anime no cuenta con ningun episodio aun.'}
	<span
		style="display:inline-block;margin-left: 20px;margin-top: 20px;margin-bottom: 20px;font-size: 1.2rem;font-weight: bold;"
		>Aun no hay ningun episodio subido.</span
	>
{:else}
	<section class="list">
		{#each data as episode}
			<a href={`/anime/episodio/${animeId}/${episode.episodeNumber}`} class="item">
				<div class="info">
					<img
						src={episode.thumbnail}
						class="thumbnail"
						loading="lazy"
						alt={`episodio ${episode.episodeNumber}`}
					/>
					<span class="text">Episodio {episode.episodeNumber} </span>
				</div>
				<div style="height: 1px; background-color:#666;margin-bottom: 2px;margin-top: 2px;" />
			</a>
		{/each}
	</section>
{/if}

<style type="text/css">
	* {
		transition: 0.5s;
	}
	.list {
		margin-top: 80px;
		margin-right: 8px;

		max-width: 100%;
	}
	.item {
		text-decoration: none;
	}
	.item .info {
		width: 100%;
		margin-left: 8px;
		display: flex;
		flex-direction: row;
		align-items: center;
		cursor: pointer;
	}
	.item .info:hover {
		opacity: 0.3;
	}
	.item .thumbnail {
		width: 120px;
		height: 70px;
		object-fit: cover;
		margin-right: 10px;
	}
	.item .text {
		font-size: 1.2rem;
		font-weight: bold;
	}
</style>
