<!-- A general layout provider -> Base for future improvements -->
<script lang="ts">
    //Math
	import type { Snippet } from 'svelte';
	let { left, center, right, classIn, idIn }: { left?: Snippet; center?: Snippet; right?: Snippet, classIn?: string, idIn?: string } = $props();
</script>

<!-- Must-Have -->
<div class="{classIn} layout" id={idIn}>
    {#if left}<div class="left-side">{@render left()}</div>{/if}
	{#if center}<div class="center">{@render center()}</div>{/if}
	{#if right}<div class="right-side">{@render right()}</div>{/if}
</div>
