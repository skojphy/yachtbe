<script>
	const MAX_ROLLS = 3;

	let dice = Array.from({ length: 5 }, (_, i) => ({ id: i + 1, value: 0, isStored: false }));
	let storedDice = [];
	let rollsLeft = MAX_ROLLS;
	let showExitButton = false;

	const getRandomDiceValue = () => Math.floor(Math.random() * 6) + 1;

	const rollDice = () => {
		if (rollsLeft <= 0) return null;

		dice = [...dice].map((die) => (die.isStored ? die : { ...die, value: getRandomDiceValue() }));
		rollsLeft -= 1;

		if (rollsLeft === 0) showExitButton = true;
	};

	const toggleStoreDice = (id) => {
		const index = id - 1;
		dice[index].isStored = !dice[index].isStored;
		storedDice = dice.filter((die) => die.isStored).sort((a, b) => a.value - b.value);
	};

	const resetDice = () => {
		dice = Array.from({ length: 5 }, (_, i) => ({ id: i + 1, value: 0, isStored: false }));
		storedDice = [];
		rollsLeft = MAX_ROLLS;
		showExitButton = false;
	};
</script>

<main>
	<h1>Yachtsbe</h1>

	<div class="dice-container">
		<h2>주사위</h2>
		{#each dice as { id, value, isStored } (id)}
			<button class={`dice ${isStored ? 'stored' : ''}`} on:click={() => toggleStoreDice(id)}
				>{#if value === 1}
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
				{/if}</button
			>
		{/each}
	</div>

	<button class="button roll-button" on:click={rollDice}>굴리기</button>
	{#if showExitButton}
		<button class="button exit-button">종료하기</button>
	{/if}
	<button class="button reset-button" on:click={resetDice}>다시 굴리기</button>

	<div class="info">
		<h2>안내</h2>
		<p>보관할 주사위를 클릭해 주세요.</p>
		<p>보관된 주사위를 클릭하면 다시 굴릴 수 있습니다.</p>
	</div>

	<div class="stored-dice-container">
		<h2>주사위 보관소 👉</h2>
		<div class="stored-dice">
			<div>보관주사위1</div>
		</div>
	</div>

	<div class="results">
		<h2>평가 결과</h2>
		<p>결과1</p>
	</div>
</main>

<style>
	.dice-container {
		display: flex;
	}

	.dice {
		position: relative;
		width: 60px;
		height: 60px;
		background-color: white;
		border: 1px solid #ccc;
		border-radius: 5px;
		display: flex;
		justify-content: center;
		align-items: center;
		font-size: 20px;
		font-weight: bold;
		margin: 0 10px;
	}

	.stored {
		border: 2px solid rgb(255, 110, 110);
	}

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

	.button {
		margin-top: 10px;
		font-size: 18px;
		cursor: pointer;
		border: none;
		border-radius: 5px;
		padding: 10px 20px;
	}

	.roll-button {
		background-color: #6cbdff;
		color: #fff;
	}

	.exit-button {
		background-color: rgb(242, 89, 89);
		color: #fff;
	}

	.reset-button {
		background-color: #78d77c;
		color: #fff;
	}

	.info {
		margin-top: 10px;
		font-size: 16px;
	}

	.stored-dice-container {
		margin-top: 20px;
		display: flex;
	}
</style>
