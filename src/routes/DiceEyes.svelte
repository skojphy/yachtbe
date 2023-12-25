<script>
	export let value;
</script>

{#if value === 1}
	<div class="dot center"></div>
{:else if value === 2}
	<div class="dot top-left"></div>
	<div class="dot bottom-right"></div>
{:else if value === 3}
	<div class="dot top-left"></div>
	<div class="dot center"></div>
	<div class="dot bottom-right"></div>
{:else if value === 4}
	<div class="dot top-left"></div>
	<div class="dot top-right"></div>
	<div class="dot bottom-left"></div>
	<div class="dot bottom-right"></div>
{:else if value === 5}
	<div class="dot top-left"></div>
	<div class="dot top-right"></div>
	<div class="dot center"></div>
	<div class="dot bottom-left"></div>
	<div class="dot bottom-right"></div>
{:else if value === 6}
	<div class="dot top-left"></div>
	<div class="dot top-center"></div>
	<div class="dot top-right"></div>
	<div class="dot bottom-left"></div>
	<div class="dot bottom-center"></div>
	<div class="dot bottom-right"></div>
{/if}

<style>
	.dot {
		width: 10px;
		height: 10px;
		background-color: #000;
		border-radius: 50%;
		position: absolute;
	}

	.top-left {
		top: 20%;
		left: 20%;
	}

	.top-right {
		top: 20%;
		right: 20%;
	}

	.top-center {
		top: 20%;
		right: 40%;
	}

	.center {
		top: 40%;
		left: 40%;
	}

	.bottom-left {
		bottom: 20%;
		left: 20%;
	}

	.bottom-right {
		bottom: 20%;
		right: 20%;
	}

	.bottom-center {
		bottom: 20%;
		right: 40%;
	}
</style>
