<script context="module">
	export async function load({ page }) {
		console.log('Fetching', page);
		const res = await fetch(
			`https://cdn.builder.io/api/v2/content/page?apiKey=7586388966a8498d98024cc1a85db023&userAttributes.urlPath=${page.path}&limit=1&fields=id,data.title`
		);
		const json = await res.json();
		const id = json?.results?.[0]?.id;
		if (!id) {
			console.log('404 it');
			return false;
		}

		let builder = json?.results?.[0];
		console.log('Builder', JSON.stringify(builder));

		return {
			props: {
				builder
			}
		};
	}
</script>

<script>
	export let builder;
	import { onMount } from 'svelte';
	let BuilderPage;
	let AboutPage;

	onMount(async () => {
		BuilderPage = (await import('$lib/BuilderPage.svelte')).default;
		if (builder?.data?.title == 'About') AboutPage = (await import('$lib/About.svelte')).default;
	});
</script>

<svelte:head>
	<title>{builder?.data?.title}</title>
	<script async src="https://cdn.builder.io/js/webcomponents"></script>
</svelte:head>

<svelte:component this={BuilderPage} />
<svelte:component this={AboutPage} />
