<script>
	// @ts-nocheck

	const DWIDTH = 1536;
	const DHEIGHT = 740;

	import { onMount, tick } from 'svelte';

	let canvas;

	onMount(async () => {
		const hydraModule = await import('hydra-synth');
		const Hydra = hydraModule.default;

		const h = new Hydra({
			canvas: canvas,
			makeGlobal: false,
			detectAudio: false
		}).synth;

		h.osc(24, 0, 0.037)
			.kaleid()
			.mask(h.shape(5, 0.03, 1))
			.modulateRotate(h.shape(1.782, 0.15, 0.032))
			.modulateRotate(h.shape(2, 0.01, 5.304))
			.modulateRotate(h.shape(3, 0.001, 2.045))
			.scale(0.6)
			.mult(h.shape(4, 0.2, 1).color(0.1, 0.01, 0.1, 0.5))
			.rotate(() => h.time * 0.039)
			.out();
		h.render();
	});
</script>

<div class="w-screen h-screen grid place-content-center bg-black">
	<canvas class="fixed" bind:this={canvas} width={DWIDTH * 2} height={DHEIGHT * 2} />
	<h1 class="font-extrabold text-3xl mix-blend-lighten text-red-900">
		hey, eugene here! <br />
		wanna see some cool wwweb magic? <br />
		(ﾉ≧∀≦)ﾉ・‥…炎炎炎炎炎炎炎炎
	</h1>
</div>
