<script lang="ts">
	import { connected, web3, selectedAccount, chainId, chainData } from 'svelte-web3';
	// connected: store value is true if a connection has been set up.
	// web3: store value is a Web3.js instance when connected.
	// selectedAccount: store value is the current selected account (when connected).
	// chainId: store value is the current chainId when connected.
	// chainData: store value is the current blockchain CAIP-2 data (when connected), see below.
	import { defaultEvmStores as evm } from 'svelte-web3';

	
	enum ConnectAction {
		Browser = 'Browser',
		Localhost = 'Localhost',
		Localhost4 = 'Localhost4',
		Gnosis = 'Gnosis',
		Arbitrum = 'Arbitrum'
	}

	const handleOnConnect = (action: ConnectAction) => {
		switch (action) {
			case ConnectAction.Browser:
				evm.setProvider();
		}
	};


</script>

{#if $connected}
	<span>CONNECTED {$connected}</span>
	<span>selectedAccount {$selectedAccount}</span>
	<span>chainId {$chainId}</span>
	<span>chainData {$chainData}</span>
{:else}
	<button on:click={() => handleOnConnect(ConnectAction.Browser)}>Connect To Wallet</button>
{/if}
