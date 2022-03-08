<div class="container">
	<button class="button">
		<i class="fa-solid fa-heart icon" />
		<span>Favoritos</span>
	</button>
	<button class="button">
		<i class="fa-regular fa-clock icon" style="color:#bbb;" />
		<span style="color:#bbb;">Ver mas tarde</span>
	</button>
</div>

<style type="text/css">
	* {
	}
	.icon {
		margin-bottom: 5px;
	}
	.container {
		margin-top: 20px;
		width: 100%;
		display: flex;
		align-items: center;
		justify-content: center;
	}
	button.button:hover {
		opacity: 0.5;
		border-radius: 5px;
		background-color: rgba(187, 187, 187, 0.2);
	}
	button.button {
		cursor: pointer;
		background: none;
		padding: 5px;
		border: none;
		outline: none;
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		margin-right: 15px;
		font-weight: bold;
	}
</style>
