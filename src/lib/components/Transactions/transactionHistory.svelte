<script lang="ts">
	import { onMount } from 'svelte';

	import {
		Alchemy,
		AssetTransfersCategory,
		Network,
		type AssetTransfersResponse,
		// type AssetTransfersResult
	} from 'alchemy-sdk';

	let transactionsHeaders: string[] = [];
	// let transactionsData: AssetTransfersResult[] = [];
	type AssetTransfersResult ={
		to: string|null;
		from: string|null;
		asset: string|null;
		value: number | null;
	}
	let transactionsData: AssetTransfersResult[] = [];

	const transactionFieldsToDisplay = ["from", "to", "value", "asset"]

	const config = {
		apiKey: import.meta.env.VITE_ALCHEMY_API_KEY,
		network: Network.ETH_GOERLI
	};
	
	onMount(async () => {
		const alchemy = new Alchemy(config);
		const transactions: AssetTransfersResponse = await alchemy.core.getAssetTransfers({
			category: [AssetTransfersCategory.ERC20, AssetTransfersCategory.ERC721]
		});
		if (transactions && transactions.transfers) {
			transactionsHeaders = transactionFieldsToDisplay
			transactionsData = transactions.transfers.map(({from,to,value,asset}) => ({from, to, value,asset}));
		}
		debugger;
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
							{value}
						</td>
					{/each}
				</tr>
			{/each}
		</tbody><tbody />
	</table>
</figure>
