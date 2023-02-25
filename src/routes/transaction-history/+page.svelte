<script lang="ts">
	import TransactionHistory from '../../lib/components/Transactions/transactionHistory.svelte';
	import { onMount, setContext } from 'svelte';
	import { ethers } from 'ethers';
	import type { TransactionDataType } from '../../types/transaction.type';
	import {
		Alchemy,
		AssetTransfersCategory,
		Network,
		type AssetTransfersResponse
		// type AssetTransfersResult
	} from 'alchemy-sdk';

	const ethNetwork = 'ropsten'; // or mainnet;
	let transactionsHeaders: string[] = [];
	let transactionsData: TransactionDataType[];
	const CONTRACT_ADDRESS = '0xA79784b15F463c8024Bda8e379142A70e0F13c6b';
	const transactionFieldsToDisplay = ['from', 'to', 'value', 'hash'];
	const config = {
		apiKey: import.meta.env.VITE_ALCHEMY_API_KEY,
		network: Network.ETH_GOERLI
	};

	async function getTransactionsData() {
		if (!window.ethereum) {
			return;
		}
		
		const alchemy = new Alchemy(config);
		const transactions: AssetTransfersResponse = await alchemy.core.getAssetTransfers({
			category: [AssetTransfersCategory.ERC20, AssetTransfersCategory.ERC721]
		});
		
		if (transactions && transactions.transfers) {
			transactionsHeaders = transactionFieldsToDisplay;
			transactionsData = transactions.transfers.map(({ from, to, value, asset ,hash }) => ({
				from,
				to,
				value: `${value} ${asset}`,
				hash
			}));
			
		}
	}
	onMount(getTransactionsData);
</script>

<TransactionHistory headers={transactionsHeaders} transactions={transactionsData} />
