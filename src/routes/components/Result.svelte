<script>
	export let result = {};
	let resultCategories = [];

	$: {
		const {
			ones,
			twos,
			threes,
			fours,
			fives,
			sixes,
			choice,
			fourOfAKind,
			fullHouse,
			smallStraight,
			largeStraight,
			yacht
		} = result;

		resultCategories = [
			['Ones', ones],
			['Twos', twos],
			['Threes', threes],
			['Fours', fours],
			['Fives', fives],
			['Sixes', sixes],
			['Sub total', 0],
			['Bonus(35)', 0],
			['Choice', choice],
			['4 of a kind', fourOfAKind],
			['Full house', fullHouse],
			['Small straight', smallStraight],
			['Large straight', largeStraight],
			['Yacht', yacht],
			['Total', 0]
		];
	}
</script>

<table>
	<thead>
		<tr>
			<th>항목</th>
			<th>점수</th>
		</tr>
	</thead>
	<tbody>
		{#each resultCategories as [item, score] (item)}
			<tr>
				<td>{item}</td>
				<td>{score}</td>
			</tr>
		{/each}
	</tbody>
</table>

<style>
	table {
		border-collapse: collapse;
		width: 100%;
		margin: 20px 0;
	}

	th,
	td {
		border: 1px solid #ddd;
		padding: 12px;
		text-align: left;
	}

	th {
		background-color: #f2f2f2;
		font-weight: bold;
	}

	tr:nth-child(even) {
		background-color: #f9f9f9;
	}
</style>
