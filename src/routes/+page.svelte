<script lang="ts">
    // Math
	import Button from '$lib/components/Button.svelte';
	import BgHome from '$lib/assets/background_home.mp4';
	import Layout from '$lib/Layout.svelte';

	let video: HTMLVideoElement, ready = $state(false), pending = false, p = 0;

	// As user scroll's event, bg vid sync frame to match the scroll progress
	const frame_sync = () => {
	    if (video.duration) {
			pending = true;
			video.currentTime = p * video.duration;
	    }
	};
	$effect(() => {
	    // After the browser read vid data, this start
		const load_after = () => {
		    ready = true; //allow scrolling
			frame_sync(); //enrure-ing/load the first frame ...
		};
		// After the frame sync task finish, check if user scrolling again
		const frame_sync_after = () => {
		    pending = false;
			if (Math.abs(video.currentTime - p * video.duration) > 0.01) {
			  frame_sync();//sync
			};
		};
		// Scrool
		const scroll = () => {
			const m = document.body.scrollHeight - innerHeight;
			if (!ready || m <= 0) return;
			p = Math.min(Math.max(scrollY / m, 0), 1);
			if (!pending) {
			  frame_sync()//sync
			};
		};

		// Aftermath
		video.addEventListener('loadedmetadata', load_after);
		video.addEventListener('seeked', frame_sync_after);
		addEventListener('scroll', scroll, { passive: true });
		if (video.readyState >= 1) { scroll(); load_after(); }
		return () => {
		    video.removeEventListener('loadedmetadata', load_after);
			video.removeEventListener('seeked', frame_sync_after);
			removeEventListener('scroll', scroll);
		};
	});
</script>

<!-- Vid/Bg -->
<video bind:this={video} id="background-video" muted playsinline preload="auto" aria-hidden="true">
    <source src={BgHome} type='video/mp4' />
</video>

<!-- The thing that people should see first, i don't know how to express that... -->
<section id="must-see">
    <Layout classIn="content">
        {#snippet center()}
            <span class="title">Pumpkin Market</span>
          		<p class="subtitle">A martket for pump-keen</p>
          		<div class="btn-group-row">
          			<Button href="/" color="green"><i class="fa-solid fa-compass"></i>Begin Your Journey</Button>
          			<Button href="/browse" color="skin"><i class="fa-solid fa-magnifying-glass"></i>Explore Landscapes...</Button>
          		</div>
        {/snippet}
    </Layout>
</section>

<!-- The thing that people should sroll down to scroll, i don't know how to express that... -->
<section id="may-see">
    <Layout classIn="content">
        {#snippet left()}
            <span class="title">Pumpkin Market</span>
          		<p class="subtitle">A martket for pump-keen</p>
          		<div class="btn-group-row">
          			<Button href="/" color="green"><i class="fa-solid fa-compass"></i>Begin Your Journey</Button>
          			<Button href="/" color="skin"><i class="fa-solid fa-magnifying-glass"></i>Explore Landscapes...</Button>
          		</div>
        {/snippet}
    </Layout>
</section>
