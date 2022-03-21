<script>
	export let animeData;
</script>

<main class="preview-anime-information">
	<h2 class="anime-title">{animeData.name}</h2>
	<div class="details">
		<span id="type" class="badge"
			><span class="material-icons-round">live_tv</span>{animeData.type}</span
		>
		<span id="study" class="badge"
			><span class="material-icons-round"> edit </span>

			{animeData.study}</span
		>
		<span id="releaseText" class="badge"
			><span class="material-icons-round"> event </span>
			{animeData.releaseDate}</span
		>
	</div>
	{#if animeData.synopsis.length >= 800}
		<p class="synopsis">{animeData.synopsis.substring(0, 800)}...</p>
	{:else}
		<p class="synopsis">{animeData.synopsis}</p>
	{/if}
	<div class="actions">
		<a href={`/anime/${animeData.id}`} class="button" id="more-details"
			><span class="material-icons-round" style="color:inherit;"> add </span>Más detalles
		</a>

		<a href={`/anime/episodio/${animeData.id}/1`} class="button" id="watch-now"
			><span class="material-icons-round"> play_arrow </span>Ver ahora</a
		>
	</div>
</main>

<style>
	.preview-anime-information {
		max-width: 50%;
		display: flex;
		justify-content: flex-start;
		align-items: flex-start;
		margin-top: 70px;
		margin-left: 40px;
		margin-right: 40px;
		flex-direction: column;
	}
	.anime-title {
		margin-bottom: 20px;
		font-size: 3rem;
		font-weight: 500;
	}
	.synopsis {
		font-size: 1.2rem;
		font-weight: 300;
		color: #eee;
	}
	.details {
		margin-bottom: 30px;
		display: flex;
		justify-content: flex-start;
		align-items: center;
	}
	#type {
		margin-right: 10px;
	}
	#study {
		margin-right: 10px;
		margin-left: 10px;
	}
	#releaseText {
		margin-right: 10px;
		margin-left: 10px;
	}
	.actions {
		display: flex;
		margin-top: 30px;
	}
	.button {
		display: flex;
		align-items: center;

		padding-top: 10px;
		padding-bottom: 10px;
		padding-right: 20px;
		padding-left: 20px;
		font-size: 1.2rem;
		border-radius: 5px;
		font-weight: bold;
		text-decoration: none;
	}
	.button:hover {
		opacity: 0.5;
	}
	.button span.material-icons-round {
		margin-right: 10px;
	}
	#more-details {
		background: #fff;
		color: #111;
		margin-right: 10px;
	}
	#watch-now {
		background-color: #1f1f1f;
	}
	.badge {
		display: flex;
		font-weight: 300;
		font-size: 1rem;
		align-items: center;
		justify-content: center;
		padding: 7px;
		border-radius: 5px;
		border: 1px solid #666;
	}
	.badge span.material-icons-round {
		margin-right: 5px;
	}
</style>
