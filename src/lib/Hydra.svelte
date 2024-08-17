<script>
	// @ts-nocheck
	import { onMount } from 'svelte';

	let iw = $state(0);
	let ih = $state(0);

	let canvas;

	$effect(() => {
		canvas.width = iw;
		canvas.height = ih;

		updateCanvas();
	});

	async function updateCanvas() {
		const hydraModule = await import('hydra-synth');
		const Hydra = hydraModule.default;

		const h = new Hydra({
			canvas: canvas,
			makeGlobal: false,
			detectAudio: false
		}).synth;

	h.osc(20, 0.03, 1.7).kaleid().mult(h.osc(20, 0.001, 0).rotate(1.58)).blend(h.o0, 0.94).modulateScale(h.osc(10, 0),-0.03).scale(0.8, () => (1.05 + 0.1 * Math.sin(0.05*h.time))).out(h.o0)

		// h.solid(0, 0, 0)
		// 	.layer(
		// 		src(o0)
		// 			.scale(1.01)
		// 			.mask(h.shape(99).scale(1, 1, () => iw / ih))
		// 	)
		// 	.blend(
		// 		h
		// 			.shape(99)
		// 			.scale(1, 1, () => iw / ih)
		// 			.mult(h.osc(20, 0.1, 2)),
		// 		0.1
		// 	)
		// 	.out();

		// src(o0).modulateHue(src(o0).scale(1.01),1).out()

		// src(o0).scale(1.01).out()

		// src(o0).modulateRotate(src(o0).scale(1.01).hue(()=>time/9).brightness(-0.3),.01).out()

		// src(o0).modulatePixelate(src(o0).hue(()=>time/9).r().contrast(2).pixelate(32,32),1024,8).out()

		// src(o0).scale(0.99).out()
	}
</script>

<svelte:window bind:innerWidth={iw} bind:innerHeight={ih} />

<canvas class="fixed -z-10 top-0" bind:this={canvas} />
