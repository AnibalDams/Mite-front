<script type="text/javascript">
	export let dataType;
	export let data = [];
</script>

<section class="result">
	{#if data.length === 0 || $data.data === undefined}
		<span style="font-weight: bold; font-size: 1.1rem;" />
	{:else}
		{#each data.data[dataType] as anime}
			{#if anime.message}
				<span>no se encontro ningun anime</span>
			{:else}
				<a href={`/anime/${anime.id}`} class="item">
					<img class="cover" loading="lazy" alt={anime.name} src={anime.cover} />
					{#if anime.name.length >= 25}
						<span class="title">
							{anime.name.substring(0, 25)}...
						</span>
					{:else}
						<span class="title">{anime.name}</span>
					{/if}
					<span class="releaseText">Estrenado: {anime.releaseDate}</span>
				</a>
			{/if}
		{/each}
	{/if}
</section>

<style type="text/css">
	

	.result {
		display: flex;
		flex-direction: row;
		flex-wrap: wrap;
		height: fit-content;
		max-width: 100%;
		justify-content: center;
		margin-top: 20px;
	}
	.item {
		display: flex;
		flex-direction: column;

		margin-top: 5px;
		margin-bottom: 15px;
		width: 150px;
		text-decoration: none;
		text-transform: capitalize;
	}
	.item:hover {
		opacity: 0.5;
	}
	.cover {
		width: 100px;
		height: 158px;
		border-radius: 5px;
		object-fit: cover;
	}
	.title {
		margin-top: 10px;
		font-size: 18px;
	}
	span.releaseText {
		font-weight: 300;
		font-size: 15px;
	}
	.icon-button {
		margin-right: 20px;
		font-size: 1.2rem;
	}
	.icon-button:active {
		opacity: 0.5;
	}
</style>
