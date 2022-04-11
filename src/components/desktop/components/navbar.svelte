<script type="text/javascript">
	let search = '';
</script>

<nav class="navBar">
	<h1><a href="/" class="brand-logo">AnimeMite</a></h1>
	<form
		class="search-form"
		on:submit|preventDefault={() => {
			return '';
		}}
	>
		<input type="text" bind:value={search} name="search" class="input" placeholder="Buscar" />
		<a
			class="search-button"
			on:click={() => setTimeout(() => window.location.reload(), 1)}
			href={`/anime/buscar/${search}`}><span class="material-icons-round">search</span></a
		>
	</form>
	<div class="buttonGroup">
		<a href="/login" class="button">Ingresar</a>
		<a href="#" class="button">Registrarse</a>
	</div>
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
		background: #eee;
		outline: none;
		color: #111;
	}
	.input:focus {
		background: #3f3f3f;
		color: #eee;
	}
	.search-button {
		text-decoration: none;
		background: #eee;
		border: none;
		padding-left: 15px;
		padding-right: 15px;
		padding-top: 16px;
		padding-bottom: 16px;
		cursor: pointer;
		border-top-right-radius: 5px;
		border-bottom-right-radius: 5px;
	}
	.search-button span {
		color: #111;
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
	.button {
		margin: 5px;
		text-decoration: none;
		font-size: 1.3rem;
		font-weight: bold;
		padding-left: 15px;
		padding-right: 15px;
		padding-top: 10px;
		padding-bottom: 10px;
		border-radius: 5px;
	}
	.button:hover {
		background: rgba(10, 10, 10, 0.5);
	}
</style>
