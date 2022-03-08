<script>
	// import Actions from './detailsPageActions.svelte';
	import GenreList from './MobileGenreList.svelte';

	export let data;
</script>

<section class="information">
	<div class="mainInfo">
		<img src={data.cover} class="cover" loading="lazy" alt={data.name} />

		<div class="texts">
			<h2 class="title">{data.name}</h2>
			<span class="study">{data.study} • {data.releaseDate}</span>
			{#if data.onGoing}
				<span class="onGoing"><span class="material-icons-round">schedule</span>En Curso</span>
			{:else}
				<span class="onGoing"><span class="material-icons-round">done</span>Finalizado</span>
			{/if}
		</div>
	</div>
	<p style="color:#aaa; padding:5px;margin-top:20px;">
		{data.synopsis}
	</p>
	<GenreList genres={data.genres} />
</section>

<style>
	.material-icons-round {
		margin-right: 5px;
		color: #bbb;
	}
	.information {
		width: 100%;
		margin: 10px;
		margin-top: 30px;
	}
	.information .mainInfo {
		display: flex;
		align-items: center;
		flex-direction: row;
	}
	.information .cover {
		width: 100px;
		height: 150px;
		border-radius: 5px;
		object-fit: cover;
	}
	.information .cover:hover {
		filter: grayscale(50%);
	}
	.information .texts {
		margin: 10px;
	}
	.information .title {
		font-size: 1.4rem;
		font-weight: 600;
		margin-bottom: 5px;
		text-transform: capitalize;
	}
	.information .study {
		font-size: 15px;
		font-weight: bold;
		display: block;
		color: #ddd;
	}
	.information .onGoing {
		margin-top: 5px;
		font-size: 14px;
		color: #bbb;
		display: flex;
		align-items: center;
		font-weight: bold;
	}
</style>
