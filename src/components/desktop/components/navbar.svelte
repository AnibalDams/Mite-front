<script type="text/javascript">
	let search = '';
</script>

<nav class="navBar">
	<a href="/" class="brand-logo">Mite</a>
	<div class="search-form">
		<input type="text" bind:value={search} name="search" class="input" placeholder="Buscar" />
		<a
			class="search-button"
			on:click={() => setTimeout(() => window.location.reload(), 1)}
			href={`/anime/buscar/${search}`}><span class="material-icons-round">search</span></a
		>
	</div>
	<div style="width:100px;" />
</nav>

<style>
	.navBar {
		background: transparent;
		max-width: 100%;
		height: 100px;
		padding: 10px;
		display: flex;
		align-items: center;
		justify-content: space-between;
	}
	.navBar .brand-logo {
		width: 150px;
		height: 50px;
		font-size: 2rem;
		text-decoration: none;
		font-weight: bold;
	}

	.search-form {
		display: flex;
		align-items: center;
		opacity: 0.9;
	}
	.input {
		padding: 15px;
		border-top-left-radius: 5px;
		border-bottom-left-radius: 5px;
		border: none;
		font-size: 1.2rem;
		background: #fff;
		outline: none;
	}
	.input:focus {
		background: #3f3f3f;
		color: #eee;
	}
	.search-button {
		text-decoration: none;

		background: #4f4f4f;
		border: none;
		padding: 15px;
		cursor: pointer;
		border-top-right-radius: 5px;
		border-bottom-right-radius: 5px;
	}
	.search-form:hover {
		opacity: 0.95;
	}
	.search-button:hover {
		opacity: 0.5;
	}
	.material-icons-round {
		font-size: 1.2rem;
	}
</style>
