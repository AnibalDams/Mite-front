<script>
	import cookie from 'cookie-cutter';
	import { gql, operationStore, query, mutation } from '@urql/svelte';

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
			cookie.set('profileName',null)
			
		}
	} 
</script>

<nav>
	<h1>Descubre</h1>
	<div class="icons">
		<!--<a href="#"><span class="material-icons-round">translate</span></a>-->

		{#if profileName === null || profileName === undefined || profileName === 'null'}
			<div class="buttonGroup">
				<a href="/buscar" class="button"><span class="material-icons-round">search</span></a>
				<a href="/login" class="button"><span class="material-icons-round">account_circle</span></a>
			</div>
		{:else}
			<div class="buttonGroup">
				<a href="/buscar" class="button"><span class="material-icons-round">search</span></a>
				<div class="avatarZone" style="position: relative;">
					<div
						class="dropDown"
						style="opacity: {opacity}; visibility: {opacity === 1 ? 'visible' : 'hidden'};"
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
			</div>
		{/if}
	</div>
</nav>

<style>
	h1 {
		font-size: 2rem;
		font-weight: bold;
	}
	.avatar {
		width: 40px;
		height: 40px;
		border-radius: 5px;
		object-fit: cover;
		cursor: pointer;
	}
	.avatar:hover {
		opacity: 0.5;
	}
	nav {
		background: transparent;
		padding: 15px;
		display: flex;
		flex-direction: row;
		justify-content: space-between;
		align-items: center;
		flex-wrap: wrap;
	}
	.icons {
		display: flex;
		align-items: center;
	}
	.icons a {
		text-decoration: none;
		margin-right: 10px;
		font-size: 1.5rem;
	}
	.icons a:hover {
		opacity: 0.5;
	}
	.buttonGroup {
		display: flex;
		justify-content: center;
		align-items: center;
	}
	.dropDown {
		position: absolute;
		width: 150px;
		height: 180px;
		padding: 10px;
		z-index: 9;
		display: flex;
		border-radius: 5px;
		align-items: center;
		justify-content: center;
		flex-direction: column;
		top: 110%;
		left: -250%;
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
