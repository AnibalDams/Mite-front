



<svelte:head>
	<title>Selecciona un perfil - AnimeMite</title>
</svelte:head>
<div class="container" >
	<h3>Selecciona un perfil</h3>
	<div class="profiles">
		<button class="profile">
			<img src="https://mite-api.herokuapp.com/img/gon_avatar.jpg">
			<button class="edit">
				<span class="material-icons-round" style="color:#0a0a0a;">edit</span>
			</button>
			<span class="name">Anibal</span>
		</button>
		<button class="profile">
			<img src="https://mite-api.herokuapp.com/img/luffy_avatar.jpg">
			<button class="edit">
				<span class="material-icons-round" style="color:#0a0a0a;">edit</span>
			</button>
			<span class="name">Mariana</span>
		</button>
		<button class="profile">
			<img src="https://mite-api.herokuapp.com/img/meliodas_avatar.jpg">
			<button class="edit">
				<span class="material-icons-round" style="color:#0a0a0a;">edit</span>
			</button>
			<span class="name">Peter</span>
		</button>
		<button class="profile">
			<img src="https://avatarfiles.alphacoders.com/108/108672.gif">
			<button class="edit">
				<span class="material-icons-round" style="color:#0a0a0a;">edit</span>
			</button>
			<span class="name">Maria</span>
		</button>
		<button class="profile add" title="Nuevo perfil">
			<span class="material-icons-round">add</span>


			
		</button>
		
		
	</div>
</div>




<style type="text/css">
	.container{
		width: 100%;
		height: 100%;
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		
		margin-top: 80px;
		
	}
	.container h3{
		font-size: 3rem;
	}
	.profiles{

		height: 100%;
		display: flex;
		flex-wrap: wrap;
		width: 70%;
		justify-content: center;
		align-items: center;
	}
	.profile{
			position: relative;
		cursor: pointer;
		margin: 30px;
		border: none;
		outline: none;
		background: none;
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;

	}
	.profile:hover{

		transform: translateY(-10px);
	}
	
	.profile .name{
		font-size: 1.6rem;
		margin-top: 10px;
		font-weight: bold;
	}
	.profile img{
		width: 150px;
		height: 150px;
		border-radius: 50%;
		object-fit: cover;
	}
	.profile.add{
		border-radius: 50%;

		display: flex;
		align-items: center;
		justify-content: center;
		width: 150px;
		height: 150px;
		font-size: 3rem;
		background: #1a1a1a;
	}
	.profile.add:hover .material-icons-round{
		color: #1a1a1a;

	}
	.profile.add:hover{
		background: #eeee;
	}
	.edit{
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
		cursor:pointer;
	}

	.profile:hover .edit{
		top: 60%;
		opacity: 1;


	}
	
</style>