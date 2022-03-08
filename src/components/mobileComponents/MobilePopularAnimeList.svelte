<script>
	export let data;
	let _data = [];

	$: if ($data.fetching === false) {
		_data = $data.data['mostPopularAnime'];
	}
</script>

<section class="list">
	{#if _data.length === 0}
		<div />
	{:else}
		{#each _data as anime}
			<a href={`/anime/${anime.id}`} class="item">
				<img src={anime.cover} class="cover" loading="lazy" alt={anime.name} />
				<div class="details">
					<span>{anime.name}</span>
					<div class="genres">
						{#each anime.genres as genre}
							<div><a href={`/anime/genero/${genre}`}>{genre}</a></div>
						{/each}
					</div>
				</div>
			</a>
		{/each}
	{/if}
</section>

<style>
	.list {
		width: 90%;
		display: flex;
		flex-direction: column;
		margin: 10px;
	}

	.item {
		text-decoration: none;
		display: flex;
		flex-direction: row;
		justify-content: flex-start;
		cursor: pointer;
		margin-bottom: 10px;
	}
	.item:hover {
		opacity: 0.5;
	}
	.item .cover {
		width: 80px;
		height: 120px;

		object-fit: cover;

		border-radius: 5px;
	}
	.list .item .details {
		margin-left: 10px;
	}
	.list .item .details span {
		color: #eee;
		font-size: 1.2rem;
		font-weight: bold;
	}
	.list .item .details .genres {
		margin-top: 20px;
		margin-right: 20px;
		width: 100%;
		display: flex;
		flex-wrap: wrap;
		flex-direction: row;
	}
	.list .item .details .genres div {
		padding: 5px;
		border-radius: 8px;
		margin: 5px;
		text-decoration: none;
		background-color: rgb(33, 33, 33);
	}
	.list .item .details .genres div > a {
		color: #eee;
		text-decoration: none;
		font-weight: 300;
	}
	.list .item .details .genres div > a:hover {
		opacity: 0.4;
	}
</style>
