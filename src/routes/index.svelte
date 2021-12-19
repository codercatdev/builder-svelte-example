<script>
	import { onMount } from 'svelte';
	let BuilderPage;

	onMount(async () => {
		BuilderPage = (await import('$lib/BuilderPage.svelte')).default;
	});
</script>

<svelte:head>
	<title>Home</title>
	<script async src="https://cdn.builder.io/js/webcomponents"></script>
</svelte:head>

<svelte:component this={BuilderPage} entry={'b50a2489d5db49cd856f2b36f0eb61c8'}>
	<p>Loading...</p>
</svelte:component>
