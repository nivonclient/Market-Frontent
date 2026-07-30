<script lang="ts">
	import Button from '$lib/components/Button.svelte';
	import bg from '$lib/assets/background_home.mp4'; //h264 encode

	let video: HTMLVideoElement;
	let ready = $state(false);
	let pending = false;
	let latestProgress = 0;

	const applySeek = () => {
		if (!video.duration) return;
		pending = true;
		video.currentTime = latestProgress * video.duration;
	};

	const onScroll = () => {
		if (!ready) return;
		const max = document.body.scrollHeight - window.innerHeight;
		if (max <= 0) return;
		latestProgress = Math.min(Math.max(window.scrollY / max, 0), 1);
		if (!pending) applySeek(); // Only seek if not already mid-seek/pending/during
	};

	$effect(() => {
		const onLoaded = () => { ready = true; applySeek(); };
		const onSeeked = () => {
			pending = false;
			// If scroll moved further while we were seeking, after it
			const target = latestProgress * video.duration;
			if (Math.abs(video.currentTime - target) > 0.01) applySeek();
		};
		video.addEventListener('loadedmetadata', onLoaded);
		video.addEventListener('seeked', onSeeked);
		window.addEventListener('scroll', onScroll, { passive: true });
		return () => {
			video.removeEventListener('loadedmetadata', onLoaded);
			video.removeEventListener('seeked', onSeeked);
			window.removeEventListener('scroll', onScroll);
		};
	});
</script>

<video
    bind:this={video}
    id="background-video"
    muted
    playsinline
    preload="auto"
    aria-hidden="true"
>
    <source src={bg} type='video/mp4' />
</video>

<div class="wrapper-scroll">
	<div class="layout" id="content">
		<div class="center">
			<span class="title">Pumpkin Market</span>
			<p class="subtitle">A martket for pump-keen</p>
			<div class="btn-group-row">
				<Button href="/" color="green"><i class="fa-solid fa-compass"></i>Begin Your Journey</Button>
				<Button href="/" color="skin"><i class="fa-solid fa-magnifying-glass"></i>Explore Landscapes...</Button>
			</div>
		</div>
	</div>
</div>
