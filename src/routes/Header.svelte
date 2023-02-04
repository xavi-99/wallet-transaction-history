<script>
	import { page } from '$app/stores';
	import logo from '$lib/images/svelte-logo.svg';
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
		</ul>
	</nav>

<style>
</style>
