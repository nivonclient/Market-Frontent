<!-- A general image provider -> Base for future improvements -->
<script lang="ts">
    //Math
	let { imgSrc, widthOg, heightOg, relative } : { imgSrc: string; widthOg: number; heightOg: number; relative: number } = $props();
</script>

<!-- Must-Have -->
<img src={imgSrc} style="width: {widthOg*relative}px; height: {heightOg*relative}px;" alt="Img"/>
