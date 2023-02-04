<script>
	import Header from './Header.svelte';
	import '@picocss/pico';
	import WalletConnector from '$lib/components/WalletConnector/walletConnector.svelte';
</script>


<svelte:head>
	<title>Home Page</title>
	<meta name="description" content="Svelte demo app" />
</svelte:head>

<header class="container">
	<Header />
	<WalletConnector />
</header>


<main class="container" >
	<slot />
</main>
<footer class="container" />
