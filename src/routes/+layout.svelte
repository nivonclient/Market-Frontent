<!-- In order to place a general (xception will be another +layout.svelte) style -->
<script lang="ts">
    //
	import favicon from '$lib/assets/favicon.svg';
	import Header from '$lib/components/Header.svelte'
	import '$lib/assets/styles/app.css'

	let { children } = $props();
</script>

<!-- Website Icon -->
<svelte:head>
	<link rel="icon" href={favicon} />
</svelte:head>

<!-- Header -->
<Header></Header>

<!-- Body, must be... -->
{@render children()}
