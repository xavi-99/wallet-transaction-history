<script lang="ts">
	import { ethers } from 'ethers';

	let account : string,
		walletConnected = false;

	async function connectWallet() {
		walletConnected = false;
		const { ethereum } = window;
		await ethereum
			.request({ method: 'eth_requestAccounts' })
			.then((accountList: string[]) => {
				const [firstAccount] = accountList;
				account = firstAccount;
				walletConnected = true;
			})
			.catch((error : Error) => {
				walletConnected = false;
				
			});
	}
</script>

<div>
	{#if walletConnected}
		<div>
			<span>Connected Account: {account}</span>
		</div>
	{:else}
		<button on:click={connectWallet}> Connect to Metamask </button>
	{/if}
	
</div>
