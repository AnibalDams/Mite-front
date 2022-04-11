<script type="text/javascript">
	import NavBar from '../components/navbar.svelte';

	export let image;
</script>

<svelte:head>
	<title>Iniciar Sesión - AnimeMite</title>
</svelte:head>

<div
	class="main"
	style="background-image: linear-gradient(to  top   ,rgb(13,13,13) ,transparent 50%), linear-gradient(to  right,rgb(13,13,13) ,transparent 50%),linear-gradient(to  bottom,rgb(13,13,13) ,transparent 50%),linear-gradient(to  left,rgb(13,13,13) ,transparent 50%),url({image});"
>
	<form class="form">
		<h1 style="font-size:3rem;">Iniciar Sesión</h1>
		<input type="text" class="input" placeholder="Nombre de usuario" />
		<input type="password" class="input" placeholder="contraseña" />
		<button type="submit" class="button">Iniciar Sesión</button>
		<span style="font-size:1.1rem;font-weight:bold;display: inline-block;"
			>¿No tienes una cuenta?. <a
				href="/registrarse"
				style="text-decoration: none; border-bottom: 2px solid #eee;">¡Registrate!</a
			></span
		>
	</form>
</div>

<style type="text/css">
	.main {
		max-width: 100%;
		height: 600px;
		overflow: hidden;
		background-position: center;
		background-size: cover;
	}
	.form {
		width: 100%;
		height: 100%;
		display: flex;

		justify-content: center;
		align-items: center;
		flex-direction: column;
	}
	.input {
		width: 50%;
		border: 1px solid #a0a0a0;
		padding: 20px;
		margin: 10px 0;
		font-weight: bold;
		font-size: 1.1rem;
		background: #0a0a0a;
		color: #eee;
		border-radius: 5px;
		outline: none;
	}
	.input:focus {
		background: #eee;
		color: #0a0a0a;
	}
	.button {
		margin-bottom: 20px;
		width: 50%;
		cursor: pointer;
		padding-top: 10px;
		padding-bottom: 10px;
		padding-left: 15px;
		padding-right: 15px;
		font-weight: bold;
		background: none;
		font-size: 1.2rem;
		border-radius: 5px;
		border: none;
	}

	.button:hover {
		background: rgba(5, 5, 5, 0.8);
	}
</style>
