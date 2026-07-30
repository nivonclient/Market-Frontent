<!-- A general button provider -> Ensure that button are same (No xception) -->
<script lang="ts">
    // Math
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

<!-- Must-Have -->
<a href={resolve(href)} class="btn {color}">
    {@render children()}
</a>
