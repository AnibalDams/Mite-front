<div
	style=" width:100%;display: flex;margin-top: 50px; justify-content:center; align-items: center;"
>
	<div class="loading" />
</div>

<style type="text/css">
	.loading {
		display: inline-block;
		width: 50px;
		height: 50px;

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
