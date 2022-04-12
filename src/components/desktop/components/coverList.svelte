<script type="text/javascript">
	export let data;
	export let detail;
	export let type;
	export let animeToFilter = '';
</script>

{#if type === 'normal'}
	<section class="list">
		{#each data as anime}
			<div class="item" title={anime.synopsis}>
				<a
					href={`/anime/${anime.id}`}
					class="cover"
					on:click={() => {
						if (detail) {
							setTimeout(() => {
								window.location.reload();
							}, 0.01);
						}
					}}
				>
					<img src={anime.cover} class="cover-img" loading="lazy" />
					<!--<p class="gradient" />-->
					<div class="actions">
						<a href={`/anime/${anime.id}`} class="material-icons-round button">
							play_circle_outline
						</a>
					</div>
				</a>
				<div class="info">
					{#if anime.name.length > 23}
						<a
							href={`/anime/${anime.id}`}
							class="title"
							on:click={() => {
								if (detail) {
									setTimeout(() => {
										window.location.reload();
									}, 0.1);
								}
							}}>{anime.name.substring(0, 23)}...</a
						>
					{:else}
						<a
							href={`/anime/${anime.id}`}
							class="title"
							on:click={() => {
								if (detail) {
									setTimeout(() => {
										window.location.reload();
									}, 0.1);
								}
							}}>{anime.name}</a
						>
					{/if}
					<span class="text-inf">{anime.type}</span>
					<div class="dot" />
					<span class="text-inf">{anime.releaseDate}</span>
				</div>
			</div>
		{/each}
	</section>
{:else}
	<section class="list">
		{#each data as anime}
			{#if animeToFilter != anime.name}
				<div class="item" title={anime.synopsis}>
					<a
						href={`/anime/${anime.id}`}
						class="cover"
						on:click={() => {
							if (detail) {
								setTimeout(() => {
									window.location.reload();
								}, 0.01);
							}
						}}
					>
						<img src={anime.cover} class="cover-img" loading="lazy" />
						<!--<p class="gradient" />-->
						<div class="actions">
							<a href={`/anime/${anime.id}`} class="material-icons-round button">
								play_circle_outline
							</a>
						</div>
					</a>
					<div class="info">
						{#if anime.name.length > 23}
							<a
								href={`/anime/${anime.id}`}
								class="title"
								on:click={() => {
									if (detail) {
										setTimeout(() => {
											window.location.reload();
										}, 0.1);
									}
								}}>{anime.name.substring(0, 23)}...</a
							>
						{:else}
							<a
								href={`/anime/${anime.id}`}
								class="title"
								on:click={() => {
									if (detail) {
										setTimeout(() => {
											window.location.reload();
										}, 0.1);
									}
								}}>{anime.name}</a
							>
						{/if}
						<span class="text-inf">{anime.type}</span>
						<div class="dot" />
						<span class="text-inf">{anime.releaseDate}</span>
					</div>
				</div>
			{:else}{/if}
		{/each}
	</section>
{/if}

<style>
	.list {
		max-width: 100%;
		margin: 30px;
		--auto-grid-min-size: 13rem;
		display: grid;
		grid-template-columns: repeat(auto-fill, minmax(var(--auto-grid-min-size), 1fr));
		grid-gap: 1rem;
	}
	.item {
		width: 210px;
		height: 310px;
		margin-bottom: 100px;
		border-radius: 5px;
		position: relative;
		display: flex;
		flex-direction: column;
	}
	.item .cover {
		position: relative;
		cursor: pointer;
		transition: 0.5;
	}
	.item .cover:after {
		content: '';
		width: 210px;
		visibility: hidden;
		height: 310px;
		position: absolute;
		top: 0;
		left: 0;
		right: 0;
		bottom: 0;
		background: rgba(10, 10, 10, 0.5);
	}

	.item:hover .cover:after,
	.item:hover .actions .button {
		visibility: visible;
		opacity: 1;
	}

	.item .cover .cover-img {
		width: 210px;
		height: 310px;
		object-fit: cover;
		border-radius: 5px;
	}
	.gradient {
		width: 210px;
		border-radius: 4.5px;
		height: 310px;
		position: absolute;
		top: 0;
		left: 0;
		right: 0;
		bottom: 0;

		background: linear-gradient(to top, #0a0a0a 0, transparent 60%);
	}
	.actions {
		position: absolute;
		display: flex;
		visibility: hidden;
		justify-content: center;
		align-items: center;
		font-size: 5rem;
		width: 210px;
		height: 310px;
		top: 0;
		left: 0;
		right: 0;
		bottom: 0;

		background-color: rgba(10, 10, 10, 0.8);
	}
	.actions .button {
		opacity: 0;
		z-index: 4;
		visibility: hidden;
		text-decoration: none;
	}
	.info {
		width: 100%;
		margin-top: 10px;
		padding-bottom: 20px;
	}
	.info .title {
		display: block;
		text-decoration: none;
		font-size: 1.2rem;
		font-weight: bold;
		margin-bottom: 10px;
	}
	.info .title:hover {
		opacity: 0.5;
	}
	.dot {
		display: inline-block;
		margin: 3px 6px;
		width: 4px;
		height: 4px;
		border-radius: 50%;
		background: #aaa;
	}
	.item .info span.text-inf {
		color: #aaa;
		font-weight: 300;
	}
</style>
