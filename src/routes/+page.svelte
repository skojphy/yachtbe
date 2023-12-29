<script>
	import DiceEyes from './components/DiceEyes.svelte';
	import Info from './components/Info.svelte';
	import Result from './components/Result.svelte';
	import ToolTip from './components/ToolTip.svelte';

	const MAX_ROLLS = 3;

	let dice = Array.from({ length: 5 }, (_, i) => ({ id: i + 1, value: 0, isStored: false }));
	let storedDice = [];
	let rollsLeft = MAX_ROLLS;
	let showExitButton = false;
	let showResult = false;

	const getRandomDiceValue = () => Math.floor(Math.random() * 6) + 1;

	const rollDice = () => {
		if (rollsLeft <= 0) return null;

		dice = [...dice].map((die) => (die.isStored ? die : { ...die, value: getRandomDiceValue() }));
		rollsLeft -= 1;
	};

	const toggleStoreDice = (id) => {
		if (rollsLeft === MAX_ROLLS) return;
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

	const endTurn = () => {
		showResult = true;
	};

	const countDice = (numberOfEyes) => storedDice.filter((die) => die.value === numberOfEyes).length;

	const getResult = () => {
		const diceCount = {
			ones: countDice(1),
			twos: countDice(2),
			threes: countDice(3),
			fours: countDice(4),
			fives: countDice(5),
			sixes: countDice(6)
		};
		const hasCount = (count) => Object.values(diceCount).some((value) => value === count);
		const hasValue = (value) => storedDice.includes(value);
		const totalSum = storedDice.reduce((acc, die) => acc + die.value, 0);
		const isFourOfAKind = hasCount(4) || hasCount(5);
		const isYacht = hasCount(5);
		const isFullHouse = (hasCount(3) && hasCount(2)) || hasCount(5);
		const isSmallStraight =
			[1, 2, 3, 4].every(hasValue) || [2, 3, 4, 5].every(hasValue) || [3, 4, 5, 6].every(hasValue);
		const isLargeStraight = [1, 2, 3, 4, 5].every(hasValue) || [2, 3, 4, 5, 6].every(hasValue);

		const result = {
			ones: diceCount.ones * 1,
			twos: diceCount.twos * 2,
			threes: diceCount.threes * 3,
			fours: diceCount.fours * 4,
			fives: diceCount.fives * 5,
			sixes: diceCount.sixes * 6,
			choice: totalSum,
			fourOfAKind: isFourOfAKind ? totalSum : 0,
			fullHouse: isFullHouse ? totalSum : 0,
			smallStraight: isSmallStraight ? 15 : 0,
			largeStraight: isLargeStraight ? 30 : 0,
			yacht: isYacht ? 50 : 0
		};

		return result;
	};
</script>

<main>
	<h1>Yachtsbe</h1>

	<ToolTip />

	<div class="dice-container">
		<h2 class="a11y-hidden">주사위</h2>
		{#each dice as { id, value, isStored } (id)}
			<button class={`dice ${isStored ? 'stored' : ''}`} on:click={() => toggleStoreDice(id)}>
				<DiceEyes {value} />
			</button>
		{/each}
	</div>

	<div class="buttons-container">
		<button class="button roll-button" on:click={rollDice}>굴리기</button>
		{#if showExitButton}
			<button class="button exit-button" on:click={endTurn}>종료하기</button>
		{/if}
		<button class="button reset-button" on:click={resetDice}>다시 굴리기</button>
	</div>

	<Info />

	<h2>주사위 보관소</h2>
	<div class="stored-dice-container">
		{#each storedDice as { id, value } (id)}
			<div class="stored-dice">
				<DiceEyes {value} isStored={true} />
			</div>
		{/each}
	</div>
	{#if showResult}
		<div class="results">
			<h2 class="a11y-hidden">결과</h2>
			<Result result={getResult()} />
		</div>
	{/if}
</main>

<style>
	.dice-container {
		display: flex;
		justify-content: space-between;
		margin: 20px 0;
	}

	.dice {
		position: relative;
		width: 55px;
		min-width: 55px;
		height: 55px;
		min-height: 55px;
		background-color: white;
		border: 1px solid #ccc;
		border-radius: 5px;
		display: flex;
		justify-content: center;
		align-items: center;
		font-size: 20px;
		font-weight: bold;
	}

	.stored {
		border: 2px solid rgb(255, 110, 110);
	}

	.buttons-container {
		display: flex;
		justify-content: space-evenly;
	}

	.button {
		margin-top: 10px;
		font-size: 18px;
		cursor: pointer;
		border: none;
		border-radius: 5px;
		padding: 10px 0;
		color: #fff;
		width: 100px;
	}

	.roll-button {
		background-color: #6cbdff;
	}

	.exit-button {
		background-color: rgb(255, 110, 110);
	}

	.reset-button {
		background-color: #78d77c;
	}

	.stored-dice-container {
		margin-top: 20px;
		display: flex;
		justify-content: center;
	}

	.stored-dice {
		position: relative;
		width: 50px;
		max-width: 50px;
		height: 50px;
		max-height: 50px;
		background-color: white;
		border: 1px solid #ccc;
		border-radius: 5px;
		display: flex;
		justify-content: center;
		align-items: center;
		font-size: 15px;
		margin: 0 5px;
	}
</style>
