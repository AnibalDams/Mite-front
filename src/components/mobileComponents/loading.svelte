<div
	style=" width:100%;display: flex; justify-content:center; align-items: center;"
>
	<div class="loading" />
</div>

<style type="text/css">
	.loading {
		display: inline-block;
		width: 50px;
		height: 50px;
		margin-top: 270px;margin-left: 10px;
		margin-right: 10px;

		border: 1px solid #aaa;
		border-radius: 5px;
		animation: loading infinite 2s ease;
	}
	@keyframes loading {
		from {
			transform: rotate(0);
		}
		to {
			transform: rotate(360deg);
		}
	}
</style>
