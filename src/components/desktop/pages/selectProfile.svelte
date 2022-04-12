<script type="text/javascript">
	import { gql, operationStore, query, mutation } from '@urql/svelte';
	import { onMount } from 'svelte';
	import cookie from 'cookie-cutter';
	import { toast } from '@zerodevx/svelte-toast';

	let user = '';
	let profile;
	let profileName="";
	let newProfile = false;
	let avatarSelected = "https://mite-api.herokuapp.com/img/meliodas_avatar.jpg"
	let avatars = ["https://mite-api.herokuapp.com/img/kanna_avatar.gif","https://mite-api.herokuapp.com/img/bakugo_avatar.jpg","https://mite-api.herokuapp.com/img/chopper_avatar.jpg","https://mite-api.herokuapp.com/img/deku_avatar.jpg","https://mite-api.herokuapp.com/img/franki_avatar.jpg","https://mite-api.herokuapp.com/img/nami_avatar.jpg","https://mite-api.herokuapp.com/img/robin_avatar.jpg","https://mite-api.herokuapp.com/img/sophie_avatar.jpg","https://mite-api.herokuapp.com/img/ussop_avatar.jpg","https://mite-api.herokuapp.com/img/meliodas_avatar.jpg","https://mite-api.herokuapp.com/img/luffy_avatar.jpg","https://mite-api.herokuapp.com/img/luffy_2_avatar.png","https://mite-api.herokuapp.com/img/gon_avatar.jpg","https://mite-api.herokuapp.com/img/eren_avatar.jpg","https://mite-api.herokuapp.com/img/goku_avatar.png","https://mite-api.herokuapp.com/img/zoro_avatar.jpg"]
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
		toast.push(`Perfil de ${name} seleccionado.`, {
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
const mutateProfile = mutation({
		query: `
      		mutation ($name: String!, $avatar: String!, $user:String!) {
			  newProfile(name:$name,avatar:$avatar,user:$user)

		}
    `
	});

	async function onSubmit(e) {
		if (profileName.length >0 && profileName.length <=15) {
			const createProfile = await mutateProfile({ name:profileName, avatar:avatarSelected, user });
			window.location.reload()

		}else if(profileName.length >=15){

			toast.push("El nombre no puede ser mayor a 15 caracteres.", {
						theme: {
							'--toastBackground': '#F56565',
							'--toastBarBackground': '#C53030'
						}
					});
		}
		else{
			toast.push("Ingresa un nombre para el perfil.", {
						theme: {
							'--toastBackground': '#F56565',
							'--toastBarBackground': '#C53030'
						}
					});
		}
	}
</script>

<svelte:head>
	<title>Selecciona un perfil - AnimeMite</title>
</svelte:head>

{#if $all.fetching != true && $all.data.findAllProfiles}
<nav style=" width: 100%;display:flex; justify-content:space-between; align-items:center;">
	<a
	href="/"
	style="display: inline-block;text-decoration:none; font-size:2rem;font-weight:bold; margin: 10px;"
	>Inicio</a
>

{#if newProfile}

	<button on:click={onSubmit} style="margin: 20px; border-radius: 5px; cursor: pointer; padding-left:15px;padding-right:15px;padding-top:10px;padding-bottom:10px;background:#eee;font-size: 1.1rem;font-weight: bold; color:#111; border: none; outline: none;">Crear Perfil</button>

{/if}

</nav>
	{#if newProfile}
	<div class="containerNew">
	<h2 style="font-size:2rem;">Crea un nuevo perfil</h2>
		<form class="formNew" on:submit|preventDefault={onSubmit}>
			<input type="text" name="new" class="input" bind:value={profileName}  placeholder="Nombre del perfil">
		</form>
	<h2 style="font-size:2rem; margin-top: 30px;">Selecciona un avatar</h2>
	<div class="avatarContainer">
		{#each avatars as Avatar}

			<img src={Avatar} style="border:{Avatar === avatarSelected? "2px solid #fff":"none"};" class="avatar" on:click={()=>{
				avatarSelected = Avatar
			}}>
		{/each}
		
	</div>

	</div>

	{:else}
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
					<button class="edit" title={`Editar el perfil de ${Profile.name}`}>
						<span class="material-icons-round" style="color:#0a0a0a;">edit</span>
					</button>
					<span class="name">{Profile.name}</span>
				</button>
			{/each}
			<button class="profile add" title="Nuevo perfil" on:click={()=>{
				newProfile = true
			}}>
				<span class="material-icons-round">add</span>
			</button>
		</div>
	</div>
	{/if}
	
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
	img {
		width: 150px;
		height: 150px;
		border-radius: 5px;
		object-fit: cover;
	}
	.profile.add {
		border-radius: 5px;
		margin-bottom: 70px;
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
		left: 80%;
		right: 0;
		bottom: 0;
		background: #f1f1f1;
		border-radius: 50%;
		opacity: 0;
		border: 3px solid rgb(13, 13, 13);
		cursor: pointer;
	}
	.edit:hover{
		transform: scale(1.3);
	}
	.profile:hover .edit {
		top: 65%;
		opacity: 1;
	}
	.containerNew{
		margin: 20px;
		max-width: 100%;
	}
	.input{
		background: rgba(10, 10, 10, 1.0);
		padding: 10px;
		height: 40px;
		width: 90%;
		margin-top: 20px;
		font-size: 1.5rem;
		font-weight: bold;
		border: 1px solid #a0a0a0;
		border-radius: 5px;
		outline: none;
	}
	.avatarContainer{
		width: 100%;
		display: flex;
		justify-content: flex-start;
		align-items: center;
		flex-wrap: wrap;
	}
	.avatar{
		margin-top: 20px;
		margin-right: 40px;
		cursor: pointer;
	}
	.avatar:hover{
		opacity: 0.5;
	}


</style>
