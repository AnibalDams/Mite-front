<script type="text/javascript">
	import { gql, operationStore, query } from '@urql/svelte';
	import { onMount } from 'svelte';
	import cookie from 'cookie-cutter';
	import { toast } from '@zerodevx/svelte-toast';

	let user = '';
	let profile;

	const queryAnimes = gql`
		query ($user: String!) {
			findAllProfiles(user: $user) {
				id
				name
				avatar
				user
			}
		}
	`;
	const all = operationStore(queryAnimes, { user }, { requestPolicy: 'cache-first' });
	function setProfile(name, avatar) {
		cookie.set('profileName', name);
		cookie.set('profileAvatar', avatar);
		profile = name;
		toast.push(`Perfil ${name} seleccionado`, {
			theme: {
				'--toastBackground': '#48BB78',
				'--toastBarBackground': '#2F855A'
			}
		});
	}
	onMount(() => {
		user = cookie.get('user');
		profile = cookie.get('profileName');

		$all.variables = { user };

		all.reexecute({ requestPolicy: 'network-only' });
	});
	query(all);
</script>

<svelte:head>
	<title>Selecciona un perfil - AnimeMite</title>
</svelte:head>
<a
	href="/"
	style="display: inline-block;text-decoration:none; font-size:2rem;font-weight:bold; margin: 10px;"
	>Inicio</a
>
{#if $all.fetching != true && $all.data.findAllProfiles}
	<div class="container">
		<h3>Selecciona un perfil</h3>
		<div class="profiles">
			{#each all.data.findAllProfiles as Profile}
				<button
					class="profile"
					on:click={() => {
						setProfile(Profile.name, Profile.avatar);
					}}
				>
					<img
						src={Profile.avatar}
						style={profile === Profile.name ? 'border: 2px solid #fff;' : 'border:none;'}
					/>
					<button class="edit">
						<span class="material-icons-round" style="color:#0a0a0a;">edit</span>
					</button>
					<span class="name">{Profile.name}</span>
				</button>
			{/each}
			<button class="profile add" title="Nuevo perfil">
				<span class="material-icons-round">add</span>
			</button>
		</div>
	</div>
{/if}

<style type="text/css">
	.container {
		width: 100%;
		height: 100%;
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;

		margin-top: 80px;
	}
	.container h3 {
		font-size: 3rem;
		margin: 30px;
	}
	.profiles {
		margin-top: 30px;
		height: 100%;
		display: flex;
		flex-wrap: wrap;
		width: 70%;
		justify-content: center;
		align-items: center;
	}
	.profile {
		border: none;
		position: relative;
		cursor: pointer;
		margin: 30px;
		padding: 10px;
		border-radius: 5px;
		outline: none;
		background: none;
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
	}
	.profile:active {
		opacity: 0.5;
	}
	.profile:hover {
		transform: translateY(-10px);
	}

	.profile .name {
		font-size: 1.6rem;
		margin-top: 10px;
		font-weight: bold;
	}
	.profile img {
		width: 150px;
		height: 150px;
		border-radius: 50%;
		object-fit: cover;
	}
	.profile.add {
		border-radius: 50%;
		border: none;
		display: flex;
		align-items: center;
		justify-content: center;
		width: 150px;
		height: 150px;
		font-size: 3rem;
		background: #1a1a1a;
	}
	.profile.add:hover .material-icons-round {
		color: #1a1a1a;
	}
	.profile.add:hover {
		background: #eeee;
	}
	.edit {
		position: absolute;
		display: flex;
		justify-content: center;
		align-items: center;
		width: 30px;
		height: 30px;
		top: 70%;
		left: 70%;
		right: 0;
		bottom: 0;
		background: #f1f1f1;
		border-radius: 50%;
		opacity: 0;
		border: 3px solid rgb(13, 13, 13);
		cursor: pointer;
	}

	.profile:hover .edit {
		top: 60%;
		opacity: 1;
	}
</style>
