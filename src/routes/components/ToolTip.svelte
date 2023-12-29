<span
	tooltip="주사위를 클릭하여 보관하세요. 빨간 테두리의 보관된 주사위를 클릭하면 다시 굴릴 수 있어요."
	flow="down">How to play</span
>

<style>
	span {
		margin: auto;
	}

	/* START TOOLTIP STYLES */
	[tooltip] {
		position: relative;
		cursor: help;
	}

	/* Applies to all tooltips */
	[tooltip]::before,
	[tooltip]::after {
		font-size: 0.8em;
		line-height: 1.2;
		user-select: none;
		pointer-events: none;
		position: absolute;
		display: none;
		opacity: 0;
	}
	[tooltip]::before {
		content: '';
		border: 5px solid transparent;
		z-index: 1001;
	}
	[tooltip]::after {
		content: attr(tooltip);
		min-width: 18em;
		max-width: 21em;
		white-space: wrap;
		overflow: auto;
		text-overflow: ellipsis;
		padding: 1ch 1.5ch;
		border-radius: 0.3ch;
		box-shadow: 0 1em 2em -0.5em rgba(0, 0, 0, 0.35);
		background: #333;
		color: #fff;
		z-index: 1000;
	}

	/* Make the tooltips respond to hover */
	[tooltip]:hover::before,
	[tooltip]:hover::after {
		display: block;
	}

	/* FLOW: DOWN */
	[tooltip][flow^='down']::before {
		top: 100%;
		border-top-width: 0;
		border-bottom-color: #333;
	}
	[tooltip][flow^='down']::after {
		top: calc(100% + 5px);
	}
	[tooltip][flow^='down']::before,
	[tooltip][flow^='down']::after {
		left: 50%;
		transform: translate(-50%, 0.5em);
	}

	/* KEYFRAMES */
	@keyframes tooltips-vert {
		to {
			opacity: 0.9;
			transform: translate(-50%, 0);
		}
	}

	@keyframes tooltips-horz {
		to {
			opacity: 0.9;
			transform: translate(0, -50%);
		}
	}

	[tooltip][flow^='down']:hover::before,
	[tooltip][flow^='down']:hover::after {
		animation: tooltips-vert 300ms ease-out forwards;
	}
</style>
