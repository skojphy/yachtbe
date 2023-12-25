<script>
	const MAX_ROLLS = 3;

	let dice = Array.from({ length: 5 }, (_, i) => ({ id: i + 1, value: 0, isStored: false }));
	let storedDice = [];
	let rollsLeft = MAX_ROLLS;

	const getRandomDiceValue = () => Math.floor(Math.random() * 6) + 1;

	const rollDice = () => {
		if (rollsLeft <= 0) return null;

		dice = [...dice].map((die) => ({ ...die, value: getRandomDiceValue() }));
		rollsLeft -= 1;
	};
</script>

<main>
	<h1>Yachtsbe</h1>

	<div class="dice-container">
		<h2>주사위</h2>
		{#each dice as { id, value, isStored } (id)}
			<button>{`주사위${id}: ${value}`}</button>
		{/each}
	</div>

	<button class="button roll-button" on:click={rollDice}>굴리기</button>
	<button class="button exit-button">종료하기</button>
	<button class="button reset-button">다시 굴리기</button>

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
