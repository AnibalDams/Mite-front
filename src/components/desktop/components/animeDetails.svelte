<script type="text/javascript">
	import NavBar from './navbar.svelte';
	import EpisodesList from './EpisodesList.svelte';
	export let anime;
	let genres = anime.genres.sort();
	export let episodes;
	let color = anime.onGoing ? '#04b31b' : '#333633';
	let visible = false;

</script>
<div class="full" style="visibility: {visible?"visible":"hidden"};opacity:{visible?1:0}" on:click={()=>{
	visible=false
}}>
	

<img src={anime.cover} >

</div>
<section class="information">
	<div class="left">
		<div class="img">
		<div class="coverC" on:click={()=>{
			visible=true
		}}>
			
		<img src={anime.cover} class="cover" />
		
		</div>
		</div>
		{#if episodes[0].message != 'Este anime no cuenta con ningun episodio aun.'}
			<a href={`/anime/episodio/${anime.id}/1`} class="button">Ver episodio 1</a>
		{/if}
	</div>
	<div class="right">
		<a href={`/anime/${anime.id}`} style="display:flex; align-items: center;"
			><h1 class="title">{anime.name}</h1>
			<div
				style="width:20px;height: 20px; border-radius: 50%; background-color: {color}; margin-left: 10px;"
			/></a
		>
		<div class="line" />
		<span style="color:grey; font-size:1.1rem;margin-top:30px; "
			>{anime.releaseDate} - {anime.type}</span
		>
		<div class="genres">
			{#each genres as genre}
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


		.full{
		 display: flex; /* Hidden by default */
		 justify-content: center;
		 align-items: center;
		 
 		 position: fixed; /* Stay in place */
  		z-index: 1; /* Sit on top */
  		left: 0;
  		top: 0;
  		width: 100%; /* Full width */
  		height: 100%; /* Full height */
  		overflow: auto; /* Enable scroll if needed */
 		 background-color: rgb(10,10,10); /* Fallback color */
  		background-color: rgba(10,10,10,0.9); /* Black w/ opacity */
  		opacity: 0;
  		visibility: hidden;
	}
	.full img{
		object-fit: cover;
		width: 300px;
		height: 500px;
		border-radius: 5px;
	}
	a {
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
	.coverC{
		cursor: pointer;
		position: relative;
		height: 278px;
		width: 195px;

	}
	.coverC:after{
		display: none;
		border-radius: 5px;
		top: 0;
		left: 0;
		right: 0;
		bottom: 0;
		position: absolute;
		content: "";
		text-align: center;
		height: 278px;
		width: 195px;
		background: rgba(10, 10, 10, 0.5);
		z-index: 99;
		opacity: 0;
	}
	.img:hover .coverC:after{
		display: block;
		opacity: 1;

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
	.cover:hover .middle{
		opacity: 1;
	}
</style>
