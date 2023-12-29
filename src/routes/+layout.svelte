<div class="layout">
	<slot />
</div>

<style>
	@import '$styles/reset';
	@import '$styles/font';
	@import '$styles/styles';

	.layout {
		max-width: 380px;
		height: 100vh;
		margin: 0 auto;
		padding-bottom: 1rem;
	}
</style>
