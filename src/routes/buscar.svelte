<script>
	import AnimeList from '../components/mobileComponents/AnimeList.svelte';
	import { gql, operationStore, query } from '@urql/svelte';

	let searchIndex = '';
	const queryAnimes = gql`
		query ($searchIndex: String!) {
			search(anime: $searchIndex) {
				message
				id
				name
				cover
				releaseDate
			}
		}
	`;
	const all = operationStore(queryAnimes, { searchIndex });
	//
	query(all);

	function onSubmit(e) {
		const formData = new FormData(e.target);

		const data = {};
		for (let field of formData) {
			const [key, value] = field;
			data[key] = value;
		}
		searchIndex = data.search;
		$all.variables = { searchIndex };
		query(all);
	}
</script>

<svelte:head>
	<title>Buscar - Mite</title>
</svelte:head>
<form class="form" on:submit|preventDefault={onSubmit}>
	<a href="/" class="icon-button"><span class="material-icons-round">arrow_back</span></a>
	<input type="text" name="search" placeholder="Buscar" class="search-input" />
	<button href="/buscar" class="icon-button" type="submit"
		><span class="material-icons-round">search</span></button
	>
</form>

{#if $all.fetching}
	<div class="loading" />
{:else}
	<AnimeList data={$all} dataType="search" />
{/if}

<style type="text/css">
	* {
		transition: 0.5s;
		overflow: hidden;
		color: #eee;
	}
	.form {
		width: 100%;
		margin-top: 10px;
		display: flex;
		align-items: center;
		justify-content: center;
	}

	.search-input {
		background: #222;
		border: none;
		outline: none;
		padding: 10px;
		font-size: 1.2rem;
		border-radius: 10px;
	}

	.icon-button {
		background: none;
		border: none;
		margin: 10px;
		font-size: 1.3rem;
		text-decoration: none;
	}
	.icon-button:active {
		opacity: 0.5;
	}

	.loading {
		display: inline-block;
		margin-left: 50%;
		margin-top: 100px;
		padding: 20px;
		border: 1px solid #aaa;
		border-radius: 5px;

		animation: loading infinite 2s ease-in-out;
	}
	@keyframes loading {
		from {
			transform: rotate(0);
		}
		to {
			transform: rotate(360deg);
		}
	}
</style>
