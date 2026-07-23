<script lang="ts">
    import { resolve } from '$app/paths';
    import type { Pathname } from '$app/types';
    import type { Snippet } from "svelte";

    let { href, color, children }: {
        href: Pathname;
        color?:
          "green" |
          "orange" |
          "skin"
          ;
        children: Snippet;
    } = $props();
</script>

<a href={resolve(href)} class="btn {color}">
    {@render children()}
</a>
