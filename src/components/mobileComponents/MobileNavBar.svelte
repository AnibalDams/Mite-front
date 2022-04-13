<script>
	import cookie from 'cookie-cutter';

	let profileName = cookie.get('profileName');
	let profileAvatar = cookie.get('profileAvatar');
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
				<div class="avatarZone">
					<img src={profileAvatar} class="avatar" />
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
</style>
