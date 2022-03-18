<nav class="navBar">
	<img src={''} class="brand-logo" />
	<form class="search-form">
		<input type="text" name="search" class="input" placeholder="Buscar" />
		<button class="search-button" type="submit"
			><span class="material-icons-round">search</span></button
		>
	</form>
	<div />
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
	}

	.search-form {
		display: flex;
		align-items: center;
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
		background: #4f4f4f;
		border: none;
		padding: 15px;
		cursor: pointer;
		border-top-right-radius: 5px;
		border-bottom-right-radius: 5px;
	}
	.search-button:hover {
		opacity: 0.5;
	}
	.material-icons-round {
		font-size: 1.2rem;
	}
</style>
