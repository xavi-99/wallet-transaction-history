<script lang="ts">
	import { onMount } from 'svelte';
	import editButton from '$lib/images/edit.svg';
	import {
		Alchemy,
		AssetTransfersCategory,
		Network,
		type AssetTransfersResponse
		// type AssetTransfersResult
	} from 'alchemy-sdk';

	let transactionsHeaders: string[] = [];
	// let transactionsData: AssetTransfersResult[] = [];
	type AssetTransfersResult = {
		to: string | null;
		from: string | null;
		asset: string | null;
		value: number | null;
	};
	let transactionsData: AssetTransfersResult[] = [];

	const transactionFieldsToDisplay = ['from', 'to', 'value', 'asset'];

	const config = {
		apiKey: import.meta.env.VITE_ALCHEMY_API_KEY,
		network: Network.ETH_GOERLI
	};

	const handleEditClick = (transaction: AssetTransfersResult) => {
	};

	onMount(async () => {
		const alchemy = new Alchemy(config);
		const transactions: AssetTransfersResponse = await alchemy.core.getAssetTransfers({
			category: [AssetTransfersCategory.ERC20, AssetTransfersCategory.ERC721]
		});
		if (transactions && transactions.transfers) {
			transactionsHeaders = transactionFieldsToDisplay;
			transactionsData = transactions.transfers.map(({ from, to, value, asset }) => ({
				from,
				to,
				value,
				asset
			}));
		}
	});
</script>

<figure>
	<table role="grid">
		<thead>
			{#each transactionsHeaders as header}
				<th scope="col">{header}</th>
			{/each}
		</thead>
		<tbody>
			{#each transactionsData as transaction}
				<tr>
					{#each Object.entries(transaction) as [key, value]}
						<td>
							{#if key === 'from' || key === 'to'}
								<div class="flex">
									<div>
										<button on:click={() => handleEditClick(transaction)} class="edit-tx-btn">
											<img src={editButton} alt="Edit your transaction wallet address"/>
										</button>
									</div>
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
		</tbody><tbody />
	</table>
</figure>

<style>
	.flex {
		display: flex;
		flex-direction: columns;
		align-items: center;
	}
	.flex div {
		padding: 0 10px;
	}
	.flex div button {
		margin-bottom: 0px;
	}
</style>
