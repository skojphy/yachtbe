<script>
	import DiceEyes from './DiceEyes.svelte';

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
	};

	const toggleStoreDice = (id) => {
		const index = id - 1;
		dice[index].isStored = !dice[index].isStored;
		showExitButton = dice.every((die) => die.isStored);
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
			<button class={`dice ${isStored ? 'stored' : ''}`} on:click={() => toggleStoreDice(id)}>
				<DiceEyes {value} />
			</button>
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
		{#each storedDice as { id, value } (id)}
			<div class="stored-dice">
				<DiceEyes {value} />
			</div>
		{/each}
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

	.stored-dice {
		position: relative;
		width: 40px;
		height: 40px;
		background-color: white;
		border: 1px solid #ccc;
		border-radius: 5px;
		display: flex;
		justify-content: center;
		align-items: center;
		font-size: 15px;
		margin: 0 10px;
	}
</style>
