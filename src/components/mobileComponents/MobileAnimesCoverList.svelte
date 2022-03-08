<script>
	export let data;
	let _data = [];
	export let dataName;
	$: if ($data.fetching === false) {
		_data = $data.data[dataName];
	}
</script>

<div class="scrollmenu">
	{#if _data.length === 0}
		<div />
	{:else}
		{#each _data as anime}
			<a href={`/anime/${anime.id}`} title={anime.synopsis}>
				<div class="container">
					<img src={anime.cover} loading="lazy" alt={anime.name} />

					{#if anime.name.length > 19}
						<span>{anime.name.substring(0, 19)}... </span>
					{:else}
						<span>{anime.name}</span>
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
		width: 150px;
		height: 250px;
		object-fit: cover;

		border-radius: 5px;
	}
	div.scrollmenu a img::before {
		content: '';
		width: 100%;
		height: 100%;
	}
	div.scrollmenu a span {
		margin-top: 5px;
		font-weight: 600;

		font-size: 1rem;
	}

	div.scrollmenu a:hover {
		opacity: 0.5;
	}
</style>
