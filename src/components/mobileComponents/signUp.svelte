<script type="text/javascript">
	import { gql, operationStore, mutation } from '@urql/svelte';
	import { getNotificationsContext } from 'svelte-notifications';
	import { toast } from '@zerodevx/svelte-toast';
	import cookie from 'cookie-cutter';
	import { onMount } from 'svelte';


	export let image;
	let username = '';
	let password = '';

	const { addNotification } = getNotificationsContext();
	const mutateLogin = mutation({
		query: `
      		mutation ($username: String!, $password: String!) {
			  newUser(username:$username,password:$password)

		}
    `
	});
	let getUser ="";
	onMount(()=>{
			getUser =  cookie.get('user')
	})

	async function onSubmit(e) {
		const login = await mutateLogin({ username, password });
		console.log(login)
		if (username.length > 0 && password.length > 0) {
			if (login.data.newUser) {
				if (
					login.data.newUser === 'El usuario ya esta en uso' ||
					login.data.login === 'Contraseña incorrecta'
				) {
					toast.push(login.data.newUser, {
						theme: {
							'--toastBackground': '#F56565',
							'--toastBarBackground': '#C53030'
						}
					});
				} else {
					toast.push(`¡Bienvenido(a) ${username}!`, {
						theme: {
							'--toastBackground': '#48BB78',
							'--toastBarBackground': '#2F855A'
						}
					});
					
					window.location.reload();
				}
			}
		}
	}
</script>

<svelte:head>
	<title>Iniciar Sesión - AnimeMite</title>
</svelte:head>

{#if getUser === null || getUser === undefined || getUser === "null"}
	<div
		class="main"
		style="background-image: linear-gradient(to  top   ,rgb(13,13,13) ,transparent 50%), linear-gradient(to  right,rgb(13,13,13) ,transparent 50%),linear-gradient(to  bottom,rgb(13,13,13) ,transparent 50%),linear-gradient(to  left,rgb(13,13,13) ,transparent 50%),url({image});"
	>
		<form class="form" on:submit|preventDefault={onSubmit}>
			<h1 style="font-size:3rem;">Registrarse</h1>
			<input type="text" bind:value={username} class="input" placeholder="Nombre de usuario" />
			<input type="password" class="input" bind:value={password} placeholder="contraseña" />
			<button type="submit" class="button">Registrarse</button>
			<span style="font-size:1.1rem;font-weight:bold;display: inline-block;"
				>Ya tienes una cuenta?. <a
					href="/login"
					style="text-decoration: none; border-bottom: 2px solid #eee;">¡Inicia sesión!</a
				></span
			>
		</form>
	</div>
{:else}
<span
		style="display: inline-block;font-size:2rem;font-weight: bold;margin-left:30%; margin-top: 200px;"
		>Ya has iniciado sesion. <a href="/selectProfile">Selecciona un perfil</a>
	</span>
	
{/if}

<style type="text/css">
	.main {
		max-width: 100%;
		height:600px;
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
		width: 80%;
		border: 1px solid #a0a0a0;
		padding: 20px;
		margin: 10px 0;
		font-weight: bold;
		font-size: 1.1rem;
		background: rgba(10, 10, 10, 0.9);
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
		width: 80%;
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
