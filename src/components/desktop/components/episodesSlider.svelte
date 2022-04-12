<script>
	import { Swiper, SwiperSlide } from 'swiper/svelte';
	import { Navigation, Pagination, Scrollbar, A11y } from 'swiper';
	import 'swiper/css';
	import 'swiper/css/navigation';
	import 'swiper/css/pagination';
	import 'swiper/css/scrollbar';
	// 24
	export let episodeData;
	let width;
			//on:slideChange={}
		//on:swiper={}
</script>

<svelte:window bind:innerWidth={width} />

{#if width <= 1228}
	<Swiper
		modules={[Navigation]}
		spaceBetween={50}
		slidesPerView={3}
		navigation

		style="margin:30px;"
	>
		{#each episodeData as episode}
			<SwiperSlide>
				<a
					href={`/anime/episodio/${episode.anime}/${episode.episodeNumber}`}
					style="text-decoration: none;"
				>
					<div class="item">
						<img src={episode.thumbnail} loading="lazy" />
						{#if episode.animeName && episode.animeName.length >= 25}
							<span class="title"
								>{episode.animeName.substring(0, 25)}... - {episode.episodeNumber}</span
							>
						{:else if episode.animeName === null}
							<span class="title">... - {episode.episodeNumber}</span>
						{:else}
							<span class="title">{episode.animeName} - {episode.episodeNumber}</span>
						{/if}
						<div class="play">
							<a
								href={`/anime/episodio/${episode.anime}/${episode.episodeNumber}`}
								class="material-icons-round button"
							>
								play_circle_outline
							</a>
						</div>
						<!--<p class="gradient" />-->
					</div>
				</a>
			</SwiperSlide>
		{/each}
	</Swiper>
{:else}
	<Swiper
		modules={[Navigation]}
		spaceBetween={50}
		slidesPerView={4}
		navigation

		style="margin:30px;"
	>
		{#each episodeData as episode}
			<SwiperSlide>
				<a
					href={`/anime/episodio/${episode.anime}/${episode.episodeNumber}`}
					style="text-decoration: none;"
				>
					<div class="item">
						<img src={episode.thumbnail} loading="lazy" />
						{#if episode.animeName && episode.animeName.length >= 25}
							<span class="title"
								>{episode.animeName.substring(0, 25)}... - {episode.episodeNumber}</span
							>
						{:else if episode.animeName === null}
							<span class="title">... - {episode.episodeNumber}</span>
						{:else}
							<span class="title">{episode.animeName} - {episode.episodeNumber}</span>
						{/if}
						<div class="play">
							<a
								href={`/anime/episodio/${episode.anime}/${episode.episodeNumber}`}
								class="material-icons-round button"
							>
								play_circle_outline
							</a>
						</div>
						<!--<p class="gradient" />-->
					</div>
				</a>
			</SwiperSlide>
		{/each}
	</Swiper>
{/if}

<style type="text/css">
	.item {
		position: relative;
		width: 310px;
		height: 210px;
	}
	.item:after {
		content: '';
		width: 310px;
		visibility: hidden;
		height: 210px;
		position: absolute;
		top: 0;
		left: 0;
		right: 0;
		bottom: 0;
		background: rgba(10, 10, 10, 0.5);
	}
	a:hover .item:after,
	a:hover .play .button {
		visibility: visible;
		opacity: 1;
	}
	a:hover .title {
		transform: translateY(-20px);
		visibility: visible;
		opacity: 1;
	}
	.item img {
		border-radius: 5px;
		width: 310px;
		height: 210px;
		object-fit: cover;
	}
	/*	.gradient {
		width: 310px;

		height: 210px;
		position: absolute;
		top: 0;
		left: 0;
		right: 0;
		bottom: 0;

		background: linear-gradient(to top, #0a0a0a 0, transparent 60%);
	}*/
	.title {
		font-size: 1.2rem;
		font-weight: bold;
		position: absolute;
		opacity: 0;
		visibility: hidden;
		top: 90%;
		left: 10px;
		right: 0;
		bottom: 0;
		z-index: 4;
	}
	.play {
		position: absolute;
		display: flex;
		justify-content: center;
		align-items: center;
		font-size: 5rem;
		width: 310px;
		height: 210px;
		top: 0;
		left: 0;
		right: 0;
		bottom: 0;
	}
	.play .button {
		opacity: 0;
		visibility: hidden;
		z-index: 4;
		text-decoration: none;
	}
</style>
