<!-- A general position provider -> Base for future improvements -->
<script lang="ts">
	import type { Snippet } from 'svelte';

	let {
		x = 0,
		y = 0,
		position = 'relative',
		inner
	}: {
		x?: number | string;
		y?: number | string;
		position?: 'relative' | 'absolute';
		inner: Snippet;
	} = $props();

	const toUnit = (v: number | string) => (typeof v === 'number' ? `${v}em` : v);
</script>

<div style="position: {position}; transform: translate({toUnit(x)}, {toUnit(y)});">
	{@render inner()}
</div>
