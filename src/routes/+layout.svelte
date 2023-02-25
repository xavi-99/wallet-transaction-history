<script>
	import Header from './Header.svelte';
	import '@picocss/pico';
	import Wallet from '$lib/components/Wallet/Wallet.svelte';
</script>

<svelte:head>
	<title>Home Page</title>
	<meta name="description" content="Svelte demo app" />
</svelte:head>

<header class="container">
	<Header />
	<Wallet />
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