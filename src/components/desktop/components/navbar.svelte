<script type="text/javascript">
	import { gql, operationStore, query, mutation } from '@urql/svelte';

	let search = '';
	import cookie from 'cookie-cutter';

	let opacity = 0;
	let user = cookie.get('user');
	let profileName = cookie.get('profileName');
	let profileAvatar = cookie.get('profileAvatar');
	const queryAnimes = gql`
		query ($user: String!) {
			findAllProfiles(user: $user) {
				_id
				id
				name
				avatar
				user
			}
		}
	`;
	const all = operationStore(queryAnimes, { user }, { requestPolicy: 'cache-first' });
	query(all);
	$: if ($all.fetching === false && $all.data.findAllProfiles) {
		let perfil = $all.data.findAllProfiles.find((el) => el.id === profileName);
		if (!perfil) {
			profileName = null;
		}
	} else {
		profileName = null;
	}
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

	<div
		class="dropDown"
		style="top: {opacity === 1 ? 90 : 80}%;opacity: {opacity};visibility: {opacity === 1
			? 'visible'
			: 'hidden'};"
	>
		<a class="dropDownOption" href="/milista">Mi Lista</a>
		<a class="dropDownOption" href="/selectProfile">Cambiar de perfil</a>
		<a
			class="dropDownOption"
			on:click={() => {
				cookie.set('user', null);
				cookie.set('profileName', null);
				cookie.set('profileAvatar', null);
				window.location.reload();
			}}
			style="color:red;">Cerrar sesión</a
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
	.avatar:hover {
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
