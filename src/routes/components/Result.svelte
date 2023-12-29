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
