<script lang="ts"> 
	import { onMount } from 'svelte';

	import { Alchemy, AssetTransfersCategory, Network, type AssetTransfersResult } from 'alchemy-sdk';
	
	let transactionsHeaders : string[] = [];
	let transactionsData : AssetTransfersResult[] = [];

	const config = {
		apiKey: import.meta.env.VITE_ALCHEMY_API_KEY,
		network: Network.ETH_GOERLI
	};

	onMount(async () => {
		const alchemy = new Alchemy(config);
		// Fetch transactions going into the desired address.
		const transactions = await alchemy.core.getAssetTransfers({
			category: [AssetTransfersCategory.ERC20, AssetTransfersCategory.ERC721]
		});
		transactionsHeaders = Object.keys(transactions.transfers[0]);
		transactionsData = transactions.transfers;
	});
</script>

<table>
	<thead>
		{#each transactionsHeaders as header}
			<th>{header}</th>
		{/each}
	</thead>
	<tbody>
		{#each transactionsData as transaction}
			<tr>
				{#each Object.entries(transaction) as field}
					<td>
						{field}
					</td>
		{/each}
			</tr>
		{/each}
	<tbody />
</table>
