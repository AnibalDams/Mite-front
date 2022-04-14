<script type="text/javascript">
	let search = '';
	import cookie from 'cookie-cutter';
	import { gql, operationStore, query } from '@urql/svelte';

	let opacity = 0;
	let profileName = cookie.get('profileName');
	let profileAvatar = cookie.get('profileAvatar');

	const queryProfileName = gql`
		query ($profile: String!) {
			 
  			 	selectUserProfile(id:$profile){
    				name
 				 }
		}
	`;
	const all = operationStore(queryProfileName, { profile:profileName }, { requestPolicy: 'cache-first' });
	query(all)

</script>

<nav class="navBar">
	<h1><a href="/" class="brand-logo">AnimeMite</a></h1>
	<form
		class="search-form"
		on:submit|preventDefault={() => {
			return;
		}}
	>
		<input type="text" bind:value={search} name="search" class="input" placeholder="Buscar" />
		<a
			class="search-button"
			on:click={() => setTimeout(() => window.location.reload(), 1)}
			href={`/anime/buscar/${search}`}><span class="material-icons-round">search</span></a
		>
	</form>
	<div class="dropDown" style="opacity: {opacity};visibility: {opacity === 1?"visible":"hidden"};">
		<a class="dropDownOption" href="/milista">Mi Lista</a>
		<a class="dropDownOption" href="/selectProfile">Cambiar de perfil</a>
		<a
			class="dropDownOption"
			on:click={() => {
				cookie.set('user', null);
				cookie.set('profileName', null);
				cookie.set('profileAvatar', null);
				window.location.reload();
			}} style="color:red;">Cerrar sesión</a
		>
	</div>
	{#if profileName === null || profileName === undefined || profileName === 'null'}
		<div class="buttonGroup">
			<a href="/login" class="button">Ingresar</a>
			<a href="/signup" class="button">Registrarse</a>
		</div>
	{:else}
		<div class="avatarZone">
			<img
				src={profileAvatar}
				class="avatar"
				title={$all.fetching === false? $all.data.selectUserProfile.name:"cargando"}
				on:click={() => {
					if (opacity === 0) {
						opacity = 1;
					} else {
						opacity = 0;
					}
				}}
			/>
		</div>
	{/if}
</nav>

<style>
	.navBar {
		position: relative;
		background: transparent;
		max-width: 100%;
		height: 100px;
		padding: 40px;

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
		padding-top: 15px;
		padding-left: 15px;
		padding-right: 15px;
		padding-bottom: 15px;
		border-top-left-radius: 5px;
		border-bottom-left-radius: 5px;
		border: none;
		font-size: 1.2rem;
		font-weight: bold;
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
	.avatarZone {
		position: relative;
	}

	.avatar {
		display: inline-block;
		width: 54px;
		height: 54px;
		object-fit: cover;
		cursor: pointer;
		border-radius: 5px;
		margin-top: 10px;
	}
	.avatar:hover{
		opacity: 0.5;
	}
	.dropDown {
		position: absolute;
		width: 150px;
		height: 150px;
		padding: 10px;
		z-index: 9;
		border-radius: 5px;
		display: flex;
		align-items: center;
		justify-content: center;
		flex-direction: column;
		top: 90%;
		left: 86%;
		right: 0;
		bottom: 0;
		background: rgba(15, 15, 15, 0.9);
	}
	.dropDownOption {
		display: inline-block;
		margin: 10px;
		width: 100%;
		cursor: pointer;
		text-decoration: none;
		font-weight: bold;
	}
	.dropDownOption:hover {
		opacity: 0.5;
	}
</style>
