<script lang="ts">
	import slideForest from './assets/imgSunlitForestPathWithLushGreenMoss1.png';
	import slideTerrain from './assets/img95TerrenoCampoRupanco20211.png';
	import slideVolcanoes from './assets/img1VolcanesLagoRupanco20211.png';
	import slideBeach from './assets/img79VolcanesLagoRupanco20211.png';
	import slideRiver from './assets/img146RioRupanco20212.png';
	import rupancoLetters from './assets/imgGroup4.svg';

	const slides = [
		{ img: slideForest, alt: 'Bosque nativo y musgo verde en Lago Rupanco' },
		{ img: slideTerrain, alt: 'Campo y vista panorámica a volcanes en Rupanco' },
		{ img: slideVolcanoes, alt: 'Lago Rupanco con aguas cristalinas y cordillera' },
		{ img: slideBeach, alt: 'Orilla y playa exclusiva en Lago Rupanco' },
		{ img: slideRiver, alt: 'Río Pulleufú y desembocadura en Lago Rupanco' }
	];

	let currentSlide = $state(0);
	let timer: ReturnType<typeof setInterval> | null = null;

	function startAutoPlay() {
		stopAutoPlay();
		timer = setInterval(() => {
			currentSlide = (currentSlide + 1) % slides.length;
		}, 6000);
	}

	function stopAutoPlay() {
		if (timer) {
			clearInterval(timer);
			timer = null;
		}
	}

	function goToSlide(index: number) {
		currentSlide = index;
		startAutoPlay();
	}

	$effect(() => {
		startAutoPlay();
		return () => stopAutoPlay();
	});
</script>

<section
	class="hero"
	id="hero"
	onmouseenter={stopAutoPlay}
	onmouseleave={startAutoPlay}
	aria-roledescription="carousel"
	aria-label="Carrusel principal del proyecto"
>
	<!-- Slider Background Images -->
	<div class="slider-backgrounds">
		{#each slides as slide, i}
			<div class="slide-pane" class:active={currentSlide === i}>
				<img src={slide.img} alt={slide.alt} class="slide-image" />
			</div>
		{/each}
		<div class="overlay-top"></div>
		<div class="overlay-bottom"></div>
	</div>

	<!-- Vertically Centered Hero Content -->
	<div class="hero-inner-container">
		<div class="hero-content">
			<p class="hero-eyebrow">PROYECTO EXCLUSIVO - X REGIÓN, CHILE</p>

			<div class="hero-title-container">
				<img src={rupancoLetters} alt="RUPANCO" class="hero-title-img" />
				<h1 class="sr-only">Rupanco — Dos Volcanes</h1>
			</div>

			<div class="hero-cta-wrapper">
				<a href="#contacto" class="hero-cta-btn">
					<span>SOLICITAR INFORMACIÓN</span>
				</a>
			</div>
		</div>
	</div>

	<!-- Bottom Section: Yellow Separator Line & Dots -->
	<div class="hero-bottom-container">
		<div class="bottom-inner">
			<div class="hero-carousel-dots" aria-label="Navegación del slider">
				{#each slides as _, i}
					<button
						type="button"
						class="slider-dot"
						class:active={currentSlide === i}
						onclick={() => goToSlide(i)}
						aria-label={`Ir a imagen ${i + 1}`}
					>
						<span class="dot-inner"></span>
					</button>
				{/each}
			</div>
			<div class="yellow-separator-line"></div>
		</div>
	</div>
</section>

<style>
	.hero {
		position: relative;
		width: 100%;
		height: 100vh;
		min-height: 650px;
		display: flex;
		flex-direction: column;
		justify-content: center;
		overflow: hidden;
		background: var(--color-plum);
	}

	/* Slider Backgrounds */
	.slider-backgrounds {
		position: absolute;
		inset: 0;
		width: 100%;
		height: 100%;
		z-index: 1;
	}

	.slide-pane {
		position: absolute;
		inset: 0;
		width: 100%;
		height: 100%;
		opacity: 0;
		transition: opacity 1.2s ease-in-out, transform 6s cubic-bezier(0.16, 1, 0.3, 1);
		transform: scale(1.04);
		pointer-events: none;
	}

	.slide-pane.active {
		opacity: 1;
		transform: scale(1);
		pointer-events: auto;
	}

	.slide-image {
		width: 100%;
		height: 100%;
		object-fit: cover;
		object-position: center 30%;
		filter: brightness(0.92);
	}

	.overlay-top {
		position: absolute;
		top: 0;
		left: 0;
		right: 0;
		height: 340px;
		background: linear-gradient(180deg, rgba(0, 0, 0, 0.72) 0%, rgba(0, 0, 0, 0) 100%);
		pointer-events: none;
	}

	.overlay-bottom {
		position: absolute;
		bottom: 0;
		left: 0;
		right: 0;
		height: 380px;
		background: linear-gradient(0deg, rgba(53, 30, 40, 0.95) 0%, rgba(53, 30, 40, 0.4) 60%, rgba(0, 0, 0, 0) 100%);
		pointer-events: none;
	}

	/* Vertically Centered Hero Content */
	.hero-inner-container {
		position: relative;
		z-index: 2;
		width: 100%;
		max-width: var(--content-max);
		margin: 0 auto;
		padding: 0 var(--gutter);
		display: flex;
		flex-direction: column;
		justify-content: center;
		flex: 1;
	}

	.hero-content {
		display: flex;
		flex-direction: column;
		align-items: flex-start;
		justify-content: center;
		max-width: 720px;
		padding-top: calc(var(--navbar-height) * 0.6);
	}

	.hero-eyebrow {
		font-family: var(--font-headline);
		font-size: clamp(1.15rem, 0.95rem + 1vw, 1.75rem);
		font-weight: 500;
		color: var(--color-lime);
		text-transform: uppercase;
		letter-spacing: 0.14em;
		margin: 0 0 var(--space-4) 0;
		text-shadow: 0 2px 12px rgba(0, 0, 0, 0.7);
	}

	.hero-title-container {
		width: 100%;
		max-width: 640px;
		margin-bottom: var(--space-6);
	}

	.hero-title-img {
		width: 100%;
		height: auto;
		display: block;
		filter: drop-shadow(0 4px 20px rgba(0, 0, 0, 0.6));
	}

	.hero-cta-wrapper {
		margin-top: var(--space-2);
	}

	.hero-cta-btn {
		display: inline-flex;
		align-items: center;
		justify-content: center;
		padding: var(--space-3) var(--space-8);
		border-radius: var(--radius-full);
		border: 1.5px solid var(--color-lime);
		background: transparent;
		color: var(--color-lime);
		font-family: var(--font-headline);
		font-size: var(--text-sm);
		font-weight: 500;
		letter-spacing: 0.14em;
		text-transform: uppercase;
		text-decoration: none;
		transition: all var(--dur-normal) var(--ease-out-expo);
	}

	.hero-cta-btn:hover {
		background: var(--color-lime);
		color: var(--color-plum);
		transform: translateY(-2px);
		box-shadow: var(--glow-primary);
	}

	/* Bottom Yellow Line & Slider Dots */
	.hero-bottom-container {
		position: absolute;
		bottom: var(--space-10);
		left: 0;
		right: 0;
		width: 100%;
		z-index: 5;
	}

	.bottom-inner {
		max-width: var(--content-max);
		margin: 0 auto;
		padding: 0 var(--gutter);
		position: relative;
		display: flex;
		align-items: center;
	}

	.yellow-separator-line {
		width: 100%;
		height: 1px;
		background: var(--color-lime);
		opacity: 0.45;
	}

	.hero-carousel-dots {
		position: absolute;
		right: var(--gutter);
		bottom: var(--space-4);
		display: flex;
		align-items: center;
		gap: 10px;
		z-index: 6;
	}

	/* Dots style matching screenshot: ○ ● ● ● */
	.slider-dot {
		background: transparent;
		border: none;
		padding: 4px;
		cursor: pointer;
		display: flex;
		align-items: center;
		justify-content: center;
		transition: transform var(--dur-fast) var(--ease-in-out);
	}

	.slider-dot .dot-inner {
		width: 6px;
		height: 6px;
		border-radius: var(--radius-full);
		background: var(--color-lime);
		opacity: 0.85;
		transition: all var(--dur-fast) var(--ease-in-out);
		box-shadow: 0 0 6px rgba(234, 240, 112, 0.4);
	}

	/* Active dot: hollow ring ○ */
	.slider-dot.active .dot-inner {
		width: 10px;
		height: 10px;
		border-radius: var(--radius-full);
		background: transparent;
		border: 1.5px solid var(--color-lime);
		opacity: 1;
		box-shadow: 0 0 10px rgba(234, 240, 112, 0.7);
	}

	.slider-dot:hover .dot-inner {
		transform: scale(1.3);
		opacity: 1;
	}

	.sr-only {
		position: absolute;
		width: 1px;
		height: 1px;
		padding: 0;
		margin: -1px;
		overflow: hidden;
		clip: rect(0, 0, 0, 0);
		white-space: nowrap;
		border: 0;
	}

	@media (max-width: 768px) {
		.hero {
			height: 100vh;
			height: 100dvh;
			min-height: 560px;
		}

		.hero-inner-container {
			display: flex;
			align-items: center;
			justify-content: center;
			text-align: center;
			padding: 0 var(--space-4);
		}

		.hero-content {
			align-items: center;
			text-align: center;
			margin: 0 auto;
			max-width: 100%;
			padding-top: calc(var(--navbar-height) * 0.2);
		}

		.hero-eyebrow {
			text-align: center;
			font-size: clamp(0.78rem, 0.7rem + 0.7vw, 0.98rem);
			letter-spacing: 0.12em;
			margin-bottom: var(--space-3);
			white-space: nowrap;
		}

		.hero-title-container {
			width: 100%;
			max-width: clamp(270px, 86vw, 360px);
			margin: 0 auto var(--space-5) auto;
			display: flex;
			justify-content: center;
		}

		.hero-cta-wrapper {
			display: flex;
			justify-content: center;
			width: 100%;
			margin-top: var(--space-1);
		}

		.hero-cta-btn {
			padding: 10px 32px;
			font-size: 0.92rem;
			text-align: center;
		}

		.hero-bottom-container {
			position: absolute;
			bottom: clamp(2rem, 8vh, 3.8rem);
			left: 0;
			right: 0;
			width: 100%;
			padding: 0 var(--space-6);
		}

		.bottom-inner {
			display: flex;
			flex-direction: column;
			align-items: center;
			gap: clamp(3.2rem, 12vh, 6.5rem);
			padding: 0;
			width: 100%;
		}

		.hero-carousel-dots {
			position: static;
			margin: 0 auto;
			display: flex;
			align-items: center;
			justify-content: center;
			gap: 15px;
		}

		.slider-dot {
			min-width: 28px;
			min-height: 28px;
			padding: 4px;
		}

		.slider-dot .dot-inner {
			width: 9px;
			height: 9px;
		}

		.slider-dot.active .dot-inner {
			width: 13px;
			height: 13px;
			border-width: 1.5px;
		}

		.yellow-separator-line {
			width: 100%;
			max-width: 460px;
			margin: 0 auto;
		}
	}
</style>
