<script>
	export let result = {};

	const resultCategories = [
		'Ones',
		'Twos',
		'Threes',
		'Fours',
		'Fives',
		'Sixes',
		'Sub total',
		'Bonus(35)',
		'Choice',
		'4 of a kind',
		'Full house',
		'Small straight',
		'Large straight',
		'Yacht',
		'Total'
	];
</script>

<table>
	<thead>
		<tr>
			<th>항목</th>
			<th>점수</th>
		</tr>
	</thead>
	<tbody>
		{#each resultCategories as category (category)}
			<tr>
				<td>{category}</td>
				<td>0</td>
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
