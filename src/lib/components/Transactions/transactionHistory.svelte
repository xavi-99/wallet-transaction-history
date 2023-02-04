<script>
	const tableHeaders = ['Header 1', 'Header 2', 'Header 3'];
	const transactionData = [
		{
			field1: 'field1',
			field2: 'field2',
			field3: 'field3',
			field4: 'field4'
		}
	];
</script>

<table>
	<thead>
		{#each tableHeaders as header}
			<th>{header}</th>
		{/each}
	</thead>
	<tbody />
</table>
