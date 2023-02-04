<script>
	import { page } from '$app/stores';
	import logo from '$lib/images/svelte-logo.svg';

	const toggleTheme = () => {
		let html = document.documentElement;
		const nextAttr = html.getAttribute('data-theme') === 'light' ? 'dark' : 'light';
		html.setAttribute('data-theme', nextAttr);
	};
</script>

<div class="corner">
	<img src={logo} alt="Logo" />
</div>

<nav>
	<ul>
		<li aria-current={$page.url.pathname === '/' ? 'page' : undefined}>
			<a href="/">Home</a>
		</li>
		<li aria-current={$page.url.pathname === '/transaction-history' ? 'page' : undefined}>
			<a href="/transaction-history">Transaction History</a>
		</li>
		<li>
			<button class="container-fluid" on:click={toggleTheme}>Theme</button>
		</li>
	</ul>
</nav>

<style>
</style>
