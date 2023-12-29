<script>
	export let value = 0;
	export let isStored = false;
</script>

{#if value === 1}
	<div class="dot center" class:stored={isStored}></div>
{:else if value === 2}
	<div class="dot top-left" class:stored={isStored}></div>
	<div class="dot bottom-right" class:stored={isStored}></div>
{:else if value === 3}
	<div class="dot top-left" class:stored={isStored}></div>
	<div class="dot center" class:stored={isStored}></div>
	<div class="dot bottom-right" class:stored={isStored}></div>
{:else if value === 4}
	<div class="dot top-left" class:stored={isStored}></div>
	<div class="dot top-right" class:stored={isStored}></div>
	<div class="dot bottom-left" class:stored={isStored}></div>
	<div class="dot bottom-right" class:stored={isStored}></div>
{:else if value === 5}
	<div class="dot top-left" class:stored={isStored}></div>
	<div class="dot top-right" class:stored={isStored}></div>
	<div class="dot center" class:stored={isStored}></div>
	<div class="dot bottom-left" class:stored={isStored}></div>
	<div class="dot bottom-right" class:stored={isStored}></div>
{:else if value === 6}
	<div class="dot top-left" class:stored={isStored}></div>
	<div class="dot top-center" class:stored={isStored}></div>
	<div class="dot top-right" class:stored={isStored}></div>
	<div class="dot bottom-left" class:stored={isStored}></div>
	<div class="dot bottom-center" class:stored={isStored}></div>
	<div class="dot bottom-right" class:stored={isStored}></div>
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
		left: 50%;
		transform: translateX(-50%);
	}

	.center {
		top: 50%;
		left: 50%;
		transform: translate(-50%, -50%);
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
		left: 50%;
		transform: translateX(-50%);
	}

	.stored {
		width: 8px;
		height: 8px;
	}
</style>
