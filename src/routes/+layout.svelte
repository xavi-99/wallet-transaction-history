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


<main class="container-fluid" >
	<slot />
</main>
<footer class="container" />

<style>
	main{
		width:95%;
		margin:0 auto;
	}
</style>