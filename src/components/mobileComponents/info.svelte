<script>
	 import Actions from './detailsPageActions.svelte';
	import GenreList from './MobileGenreList.svelte';

	export let data;
	let visible = false;
	let width;
</script>

<svelte:window bind:innerWidth={width} />

<div
	class="full"
	style="visibility: {visible ? 'visible' : 'hidden'};opacity:{visible ? 1 : 0}"
	on:click={() => {
		visible = false;
	}}
>
	<img
		src={data.cover}
		style="width: {width <= 310 ? 270 : 300}px;height: {width <= 310 ? 470 : 500}px;"
	/>
</div>

<section class="information">
	<div class="mainInfo">
		<img
			src={data.cover}
			on:click={() => {
				visible = true;
			}}
			class="cover"
			loading="lazy"
			alt={data.name}
		/>

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
		<Actions anime={data.id} animeData={data}/>
	<p style="color:#aaa; padding:5px;margin-top:20px;">
		{data.synopsis}
	</p>
	<GenreList genres={data.genres} />
</section>

<style>
	.full {
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
		background-color: rgb(10, 10, 10); /* Fallback color */
		background-color: rgba(10, 10, 10, 0.5); /* Black w/ opacity */
		opacity: 0;
		visibility: hidden;
	}
	.full img {
		object-fit: cover;
		border-radius: 5px;
	}
	.material-icons-round {
		margin-right: 5px;
		color: #bbb;
	}
	.information {
		max-width: 100%;
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
