<script lang="ts">
	import editButton from '$lib/images/edit.svg';
	import type { TransactionDataType } from '../../../types/transaction.type';

	export let headers: string[];
	export let transactions: TransactionDataType[];

	debugger;
	const handleEditClick = (transaction: TransactionDataType) => {};
</script>

<figure>
	<table role="grid">
		<thead>
			{#each headers as header}
				<th scope="col">{header}</th>
			{/each}
		</thead>
		<tbody>
			{#if transactions}
			{#each transactions as transaction}
				<tr>
					{#each Object.entries(transaction) as [key, value]}
						<td>
							{#if key === 'from' || key === 'to'}
								<div class="flex">
									<button on:click={() => handleEditClick(transaction)} class="edit-tx-btn">
										<img src={editButton} alt="Edit your transaction wallet address" />
									</button>
									<div>
										{value}
									</div>
								</div>
							{:else}
								{value}
							{/if}
						</td>
					{/each}
				</tr>
			{/each}
			{/if}
		</tbody>
	</table>
</figure>

<style>
	.flex {
		display: flex;
		flex-direction: columns;
		align-items: center;
		justify-content: center;
	}
	.flex div {
		padding: 0 10px;
	}
	table {
		font-size: 0.8em;
	}
</style>
