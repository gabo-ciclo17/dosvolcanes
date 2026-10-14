<script lang="ts">
	import badgeImg from './assets/imgCapa1.svg';
	import imgHectareas from './assets/imgTerrenoCenital51.png';
	import imgOrilla from './assets/img1VolcanesLagoRupanco20211.png';
	import imgLotes from './assets/imgTerrenoCenital52.png';
	import imgAgua from './assets/img146RioRupanco20212.png';

	interface FeatureItem {
		title: string;
		desc: string;
		img: string;
		alt: string;
	}

	const features: FeatureItem[] = [
		{
			title: '64.9 HECTÁREAS',
			desc: 'Un espacio único de naturaleza virgen, bosques nativos y paisajes inigualables.',
			img: imgHectareas,
			alt: 'Terreno cenital de 64.9 hectáreas en Rupanco'
		},
		{
			title: 'ORILLA DE LAGO',
			desc: 'Acceso privilegiado al Lago Rupanco con extensa playa de piedra y arena.',
			img: imgOrilla,
			alt: 'Orilla de lago Rupanco con vista a los volcanes'
		},
		{
			title: '28 LOTES EXCLUSIVOS',
			desc: 'Parcelas con ROL propio y servidumbre inscrita para total seguridad legal.',
			img: imgLotes,
			alt: 'Lotes exclusivos de parcelas en Dos Volcanes'
		},
		{
			title: 'DERECHOS DE AGUA',
			desc: 'Recursos hídricos propios garantizados para la tranquilidad de tu inversión.',
			img: imgAgua,
			alt: 'Río Rupanco con derechos de agua inscritos'
		}
	];

	let activeIndex = $state(0);
	let carouselEl: HTMLElement | null = $state(null);

	function handleScroll() {
		if (!carouselEl) return;
		const cards = carouselEl.querySelectorAll<HTMLElement>('.feature-card');
		if (!cards.length) return;
		const scrollLeft = carouselEl.scrollLeft;
		let closest = 0;
		let minDiff = Infinity;
		cards.forEach((card, idx) => {
			const diff = Math.abs(scrollLeft - card.offsetLeft);
			if (diff < minDiff) {
				minDiff = diff;
				closest = idx;
			}
		});
		activeIndex = closest;
	}

	function scrollToCard(index: number) {
		if (!carouselEl) return;
		const cards = carouselEl.querySelectorAll<HTMLElement>('.feature-card');
		if (cards[index]) {
			cards[index].scrollIntoView({
				behavior: 'smooth',
				block: 'nearest',
				inline: 'start'
			});
			activeIndex = index;
		}
	}
</script>

<section
	class="features-section"
	id="proyecto"
	aria-roledescription="carousel"
	aria-label="Características del proyecto"
>
	<div class="container">
		<header class="section-header">
			<div class="badge-wrapper">
				<img src={badgeImg} alt="Rupanco" class="badge-icon" />
			</div>
			<h2 class="section-title">
				EXCLUSIVIDAD Y NATURALEZA<br class="desktop-break" />
				EN UN SOLO LUGAR
			</h2>
		</header>

		<!-- Cards Grid on Desktop / Snap Carousel on Mobile -->
		<div
			class="features-grid"
			bind:this={carouselEl}
			onscroll={handleScroll}
			role="region"
			aria-label="Carrusel de características"
		>
			{#each features as item, i}
				<article class="feature-card" aria-label={`Característica ${i + 1}: ${item.title}`}>
					<div class="card-media">
						<img src={item.img} alt={item.alt} class="card-image" loading="lazy" />
					</div>
					<div class="card-body">
						<h3 class="card-title">{item.title}</h3>
						<p class="card-desc">{item.desc}</p>
					</div>
				</article>
			{/each}
		</div>

		<!-- Mobile Carousel Navigation Dots (○ ● ● ●) -->
		<div class="carousel-dots" aria-label="Navegación del carrusel">
			{#each features as _, i}
				<button
					type="button"
					class="carousel-dot"
					class:active={activeIndex === i}
					onclick={() => scrollToCard(i)}
					aria-label={`Ir a tarjeta ${i + 1}`}
				>
					<span class="dot-inner"></span>
				</button>
			{/each}
		</div>
	</div>
</section>

<style>
	.features-section {
		background: var(--color-plum);
		padding: var(--section-pad-lg) var(--gutter);
		position: relative;
		overflow: hidden;
	}

	.container {
		max-width: var(--content-max);
		margin: 0 auto;
		display: flex;
		flex-direction: column;
		align-items: center;
		gap: var(--space-12);
	}

	.section-header {
		text-align: center;
		display: flex;
		flex-direction: column;
		align-items: center;
		gap: var(--space-4);
	}

	.badge-wrapper {
		display: flex;
		align-items: center;
		justify-content: center;
		opacity: 0.95;
	}

	.badge-icon {
		height: 20px;
		width: auto;
		display: block;
	}

	.section-title {
		font-family: var(--font-headline);
		font-size: clamp(1.8rem, 1.4rem + 1.8vw, 3rem);
		font-weight: 500;
		line-height: 1.15;
		color: var(--color-ecru);
		text-transform: uppercase;
		letter-spacing: 0.04em;
		margin: 0;
	}

	.desktop-break {
		display: inline;
	}

	.features-grid {
		display: grid;
		grid-template-columns: repeat(4, 1fr);
		gap: var(--space-6);
		width: 100%;
	}

	.feature-card {
		background: var(--color-ecru);
		border-radius: var(--radius-lg);
		overflow: hidden;
		display: flex;
		flex-direction: column;
		height: 100%;
		box-shadow: 0 12px 32px rgba(0, 0, 0, 0.25);
		transition: transform var(--dur-normal) var(--ease-out-expo),
			box-shadow var(--dur-normal) var(--ease-out-expo);
	}

	.feature-card:hover {
		transform: translateY(-6px);
		box-shadow: 0 20px 40px rgba(0, 0, 0, 0.35);
	}

	.card-media {
		position: relative;
		width: 100%;
		height: 155px;
		overflow: hidden;
		background: rgba(53, 30, 40, 0.1);
	}

	.card-image {
		width: 100%;
		height: 100%;
		object-fit: cover;
		transition: transform var(--dur-slow) var(--ease-out-expo);
	}

	.feature-card:hover .card-image {
		transform: scale(1.05);
	}

	.card-body {
		padding: var(--space-6) var(--space-6) var(--space-8) var(--space-6);
		display: flex;
		flex-direction: column;
		gap: var(--space-2);
		flex: 1;
	}

	.card-title {
		font-family: var(--font-headline);
		font-size: 1.25rem;
		font-weight: 700;
		color: var(--color-plum);
		text-transform: uppercase;
		letter-spacing: 0.02em;
		margin: 0;
		line-height: 1.25;
	}

	.card-desc {
		font-family: var(--font-body);
		font-size: 0.95rem;
		line-height: 1.45;
		color: var(--color-plum);
		opacity: 0.85;
		margin: 0;
	}

	.carousel-dots {
		display: none;
	}

	@media (max-width: 1100px) {
		.features-grid {
			grid-template-columns: repeat(2, 1fr);
		}
	}

	@media (max-width: 768px) {
		.features-section {
			padding: var(--section-pad-md) 0 var(--space-10) 0;
			overflow: hidden;
		}

		.container {
			max-width: 100%;
			padding: 0;
			gap: var(--space-8);
			width: 100%;
		}

		.section-header {
			padding: 0 var(--space-6);
		}

		.section-title {
			max-width: 330px;
			margin: 0 auto;
			font-size: clamp(1.85rem, 1.55rem + 1.8vw, 2.4rem);
			line-height: 1.15;
			letter-spacing: 0.04em;
			text-align: center;
		}

		.desktop-break {
			display: none;
		}

		.features-grid {
			display: flex;
			grid-template-columns: none;
			overflow-x: auto;
			scroll-snap-type: x mandatory;
			scroll-behavior: smooth;
			-webkit-overflow-scrolling: touch;
			scrollbar-width: none;
			gap: 22px;
			padding: var(--space-2) 36px var(--space-4) 36px;
			scroll-padding-left: 36px;
			width: 100%;
			box-sizing: border-box;
		}

		.features-grid::-webkit-scrollbar {
			display: none;
		}

		.feature-card {
			flex: 0 0 264px;
			width: 264px;
			min-width: 264px;
			height: 289px;
			scroll-snap-align: start;
			scroll-snap-stop: normal;
			box-shadow: 0 10px 24px rgba(0, 0, 0, 0.32);
		}

		.feature-card:hover {
			transform: none;
		}

		.card-media {
			height: 131px;
		}

		.card-body {
			padding: 20px 20px 22px 20px;
			gap: 6px;
		}

		.card-title {
			font-size: 1.35rem;
			line-height: 1.2;
		}

		.card-desc {
			font-size: 0.95rem;
			line-height: 1.35;
		}

		.carousel-dots {
			display: flex;
			align-items: center;
			justify-content: center;
			gap: 16px;
			margin-top: var(--space-3);
		}

		.carousel-dot {
			background: transparent;
			border: none;
			min-width: 32px;
			min-height: 32px;
			padding: 6px;
			cursor: pointer;
			display: flex;
			align-items: center;
			justify-content: center;
			transition: transform var(--dur-fast) var(--ease-in-out);
			touch-action: manipulation;
		}

		.carousel-dot .dot-inner {
			width: 10px;
			height: 10px;
			border-radius: var(--radius-full);
			background: var(--color-ecru);
			opacity: 0.85;
			transition: all var(--dur-fast) var(--ease-in-out);
		}

		/* Active dot: hollow ecru ring ○ matching Figma */
		.carousel-dot.active .dot-inner {
			width: 14px;
			height: 14px;
			border-radius: var(--radius-full);
			background: transparent;
			border: 1.5px solid var(--color-ecru);
			opacity: 1;
			box-shadow: 0 0 10px rgba(225, 221, 209, 0.45);
		}

		.carousel-dot:hover .dot-inner {
			transform: scale(1.2);
			opacity: 1;
		}
	}
</style>
