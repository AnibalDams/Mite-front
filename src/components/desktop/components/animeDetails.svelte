<script type="text/javascript">
	import NavBar from './navbar.svelte';
	import EpisodesList from './EpisodesList.svelte';
	export let anime;
	export let episodes;
</script>

<section class="information">
	<div class="left">
		<img src={anime.cover} class="cover" />
		{#if episodes[0].message != 'Este anime no cuenta con ningun episodio aun.'}
			<a href={`/anime/episodio/${anime.id}/1`} class="button">Ver episodio 1</a>
		{/if}
	</div>
	<div class="right">
		<a href={`/anime/${anime.id}`}><h2 class="title">{anime.name}</h2></a>
		<div class="line" />
		<span style="color:grey; font-size:1.1rem;margin-top:30px; "
			>{anime.releaseDate} - {anime.type}</span
		>
		<div class="genres">
			{#each anime.genres as genre}
				<a href={`/anime/genero/${genre}`} class="genre">{genre}</a>
			{/each}
		</div>
		<p style="margin-top: 50px;margin-bottom: 30px;font-size: 1.1rem;">{anime.synopsis}</p>
		<div class="line" />
		<div class="details">
			<span id="estudio">Estudio</span>
			<span>{anime.study}</span>
		</div>
		<span style="font-size: 1.8rem; font-weight: bold; margin-top: 50px;">Episodios</span>
		<EpisodesList {episodes} />
	</div>
</section>

<style type="text/css">
	a{
		text-decoration: none;
	}
	.information {
		margin: 50px;
		display: flex;
		flex-direction: row;
	}
	.left {
		display: flex;
		flex-direction: column;
		align-items: center;
	}
	.cover {
		height: 278px;
		width: 195px;
		object-fit: cover;
		border-radius: 5px;
	}
	.button {
		text-decoration: none;
		margin-top: 20px;
		padding-top: 20px;
		padding-bottom: 20px;
		width: 195px;
		color: #333;
		font-size: 1.2rem;
		font-weight: bold;
		text-align: center;
		background: #ffff;
		border-radius: 5px;
	}
	.button:hover {
		opacity: 0.5;
	}
	.right {
		width: 100%;
		padding-left: 30px;
		padding-right: 30px;

		display: flex;
		flex-direction: column;
		align-items: flex-start;
		justify-content: flex-start;
	}
	.line {
		height: 1px;
		width: 100%;
		opacity: 0.2;
		background: #fff;
	}
	.right .title {
		font-size: 4rem;
		margin-top: 10px;
		margin-bottom: 30px;
	}
	.genres {
		margin-top: 40px;
	}
	.genre {
		padding-top: 5px;
		padding-bottom: 5px;
		font-weight: 300;
		margin-right: 10px;
		padding-left: 8px;
		padding-right: 8px;

		background: rgba(33, 33, 33, 0.8);
		color: white;
		text-align: center;
		border-radius: 5px;
		text-decoration: none;
	}
	.genre:hover {
		opacity: 0.5;
	}
	.details {
		margin-top: 20px;
	}
	.details span {
		font-size: 1.1rem;
		color: #ccc;
	}
	.details span#estudio {
		color: #aaa !important;
		margin-right: 30px;
	}
</style>
