<script lang="ts">
	import photoLakeView1 from './assets/imgWomanDrinkingHealthyTea2.png';
	import photoLakeView2 from './assets/img1VolcanesLagoRupanco20211.png';
	import photoLakeView3 from './assets/img79VolcanesLagoRupanco20211.png';
	import photoLakeView4 from './assets/img146RioRupanco20212.png';
	import photoLakeView5 from './assets/imgSunlitForestPathWithLushGreenMoss1.png';

	import photoForest1 from './assets/img189BosqueRupanco20211.png';
	import photoForest2 from './assets/imgSunlitForestPathWithLushGreenMoss1.png';
	import photoForest3 from './assets/imgTerrenoCenital51.png';
	import photoForest4 from './assets/imgTerrenoCenital52.png';
	import photoForest5 from './assets/img95TerrenoCampoRupanco20211.png';

	import photoShore1 from './assets/img79VolcanesLagoRupanco20211.png';
	import photoShore2 from './assets/img1VolcanesLagoRupanco20211.png';
	import photoShore3 from './assets/img146RioRupanco20212.png';
	import photoShore4 from './assets/imgWomanDrinkingHealthyTea2.png';
	import photoShore5 from './assets/img95TerrenoCampoRupanco20211.png';

	import IconZoom from '~icons/lucide/maximize-2';
	import IconX from '~icons/mynaui/x';
	import IconChevronLeft from '~icons/mynaui/chevron-left';
	import IconChevronRight from '~icons/mynaui/chevron-right';
	import badgeRegion from './assets/imgGroup.svg';
	import badgeOsorno from './assets/imgGroup1.svg';

	interface PhotoItem {
		url: string;
		alt: string;
	}

	interface GalleryCardData {
		title: string;
		desc: string;
		photos: PhotoItem[];
	}

	const cards: GalleryCardData[] = [
		{
			title: 'LAGO RUPANCO',
			desc: 'A solo 45 minutos de distancia.',
			photos: [
				{ url: photoLakeView1, alt: 'Atardecer contemplando la tranquilidad de Lago Rupanco' },
				{ url: photoLakeView2, alt: 'Vista panorámica al Lago Rupanco y cordillera' },
				{ url: photoLakeView3, alt: 'Aguas cristalinas turquesas en la bahía de Rupanco' },
				{ url: photoLakeView4, alt: 'Afluentes y desembocadura del Río Pulleufú' },
				{ url: photoLakeView5, alt: 'Sendero boscoso junto a las orillas del lago' }
			]
		},
		{
			title: 'NUESTROS BOSQUES',
			desc: 'Un espacio único de naturaleza virgen, bosques nativos y paisajes inigualables.',
			photos: [
				{ url: photoForest1, alt: 'Bosque nativo de coigües, arrayanes y robles centenarios' },
				{ url: photoForest2, alt: 'Sendero iluminado por el sol entre vegetación tupida' },
				{ url: photoForest3, alt: 'Vista aérea del follaje y reservas verdes del loteo' },
				{ url: photoForest4, alt: 'Praderas protegidas rodeadas de bosque nativo virgen' },
				{ url: photoForest5, alt: 'Mirador natural hacia los valles y volcanes del sur' }
			]
		},
		{
			title: 'ORILLA DE LAGO',
			desc: 'Un espacio único de naturaleza virgen, bosques nativos y paisajes inigualables.',
			photos: [
				{ url: photoShore1, alt: 'Extensa orilla y playa de arena fina frente al lago' },
				{ url: photoShore2, alt: 'Oleaje suave y vistas despejadas al Volcán Puntiagudo' },
				{ url: photoShore3, alt: 'Río Pulleufú con aguas puras de vertiente cordillerana' },
				{ url: photoShore4, alt: 'Refugio exclusivo con acceso privado a la ribera' },
				{ url: photoShore5, alt: 'Bahía protegida ideal para embarcaciones y kayak' }
			]
		}
	];

	// Reactive photo index for each of the 3 cards (Card 0, Card 1, Card 2)
	let activeIndices = $state<number[]>([0, 0, 0]);

	function selectCardPhoto(cardIndex: number, photoIndex: number) {
		activeIndices[cardIndex] = photoIndex;
		activeIndices = [...activeIndices];
	}

	function prevCardPhoto(cardIndex: number) {
		const total = cards[cardIndex].photos.length;
		activeIndices[cardIndex] = (activeIndices[cardIndex] - 1 + total) % total;
		activeIndices = [...activeIndices];
	}

	function nextCardPhoto(cardIndex: number) {
		const total = cards[cardIndex].photos.length;
		activeIndices[cardIndex] = (activeIndices[cardIndex] + 1) % total;
		activeIndices = [...activeIndices];
	}

	// Lightbox state tracking card index and active photo index
	let lightboxState = $state<{ cardIdx: number; photoIdx: number } | null>(null);

	function openLightbox(cardIdx: number) {
		lightboxState = {
			cardIdx,
			photoIdx: activeIndices[cardIdx]
		};
	}

	function closeLightbox() {
		lightboxState = null;
	}

	function prevLightboxPhoto() {
		if (!lightboxState) return;
		const total = cards[lightboxState.cardIdx].photos.length;
		lightboxState.photoIdx = (lightboxState.photoIdx - 1 + total) % total;
		// Sync back to card
		selectCardPhoto(lightboxState.cardIdx, lightboxState.photoIdx);
	}

	function nextLightboxPhoto() {
		if (!lightboxState) return;
		const total = cards[lightboxState.cardIdx].photos.length;
		lightboxState.photoIdx = (lightboxState.photoIdx + 1) % total;
		// Sync back to card
		selectCardPhoto(lightboxState.cardIdx, lightboxState.photoIdx);
	}
</script>

<section class="gallery-section" id="galeria">
	<div class="container">
		<header class="section-header">
			<div class="region-badge" aria-label="Región de los Lagos Osorno">
				<img src={badgeRegion} alt="Región de los Lagos" class="badge-region" />
				<img src={badgeOsorno} alt="Osorno" class="badge-osorno" />
			</div>
			<h2 class="section-title">DISFRUTA DE NUESTRA GALERÍA</h2>
			<p class="section-subtitle">
				Disfruta de las postales más lindas de nuestro lugar.
			</p>
		</header>

		<div class="gallery-grid">
			{#each cards as card, cardIdx}
				<div class="gallery-card">
					<!-- Clickable Image / Media Area -->
					<div
						class="card-media"
						onclick={() => openLightbox(cardIdx)}
						role="button"
						tabindex="0"
						onkeydown={(e) => {
							if (e.key === 'Enter' || e.key === ' ') openLightbox(cardIdx);
							if (e.key === 'ArrowLeft') prevCardPhoto(cardIdx);
							if (e.key === 'ArrowRight') nextCardPhoto(cardIdx);
						}}
						aria-label={`Ampliar imagen de ${card.title}`}
					>
						{#each card.photos as photo, pIdx}
							<img
								src={photo.url}
								alt={photo.alt}
								class="gallery-img"
								class:active={activeIndices[cardIdx] === pIdx}
								loading={pIdx === 0 ? 'eager' : 'lazy'}
							/>
						{/each}

						<!-- Hover arrows for quick cycling -->
						<button
							type="button"
							class="nav-arrow prev"
							onclick={(e) => {
								e.stopPropagation();
								prevCardPhoto(cardIdx);
							}}
							aria-label={`Foto anterior en ${card.title}`}
						>
							<IconChevronLeft style="font-size: 22px;" />
						</button>

						<button
							type="button"
							class="nav-arrow next"
							onclick={(e) => {
								e.stopPropagation();
								nextCardPhoto(cardIdx);
							}}
							aria-label={`Foto siguiente en ${card.title}`}
						>
							<IconChevronRight style="font-size: 22px;" />
						</button>

						<div class="media-overlay">
							<span class="zoom-icon">
								<IconZoom style="font-size: 20px;" />
							</span>
						</div>
					</div>

					<!-- Card Footer Content -->
					<div class="card-footer">
						<h3 class="card-title">{card.title}</h3>
						<p class="card-desc">{card.desc}</p>

						<!-- Interactive Carousel Dots per card -->
						<div class="card-dots-bar" role="tablist" aria-label={`Galería de ${card.title}`}>
							{#each card.photos as _, dotIdx}
								<button
									type="button"
									role="tab"
									class="dot-btn"
									class:active={activeIndices[cardIdx] === dotIdx}
									aria-selected={activeIndices[cardIdx] === dotIdx}
									onclick={(e) => {
										e.stopPropagation();
										selectCardPhoto(cardIdx, dotIdx);
									}}
									aria-label={`Ver foto ${dotIdx + 1} de ${card.title}`}
								>
									<span class="dot-shape"></span>
								</button>
							{/each}
						</div>
					</div>
				</div>
			{/each}
		</div>
	</div>

	<!-- Modal Lightbox -->
	{#if lightboxState !== null}
		{@const currentCard = cards[lightboxState.cardIdx]}
		{@const currentPhoto = currentCard.photos[lightboxState.photoIdx]}
		<div
			class="lightbox-overlay"
			role="dialog"
			aria-modal="true"
			aria-label="Vista ampliada de fotografía"
			tabindex="-1"
			onkeydown={(e) => {
				if (e.key === 'Escape') closeLightbox();
				if (e.key === 'ArrowLeft') prevLightboxPhoto();
				if (e.key === 'ArrowRight') nextLightboxPhoto();
			}}
		>
			<button
				type="button"
				class="lightbox-backdrop-btn"
				onclick={closeLightbox}
				aria-label="Cerrar modal"
			></button>
			<div class="lightbox-content">
				<button type="button" class="close-btn" onclick={closeLightbox} aria-label="Cerrar vista ampliada">
					<IconX style="font-size: 24px;" />
				</button>

				<button
					type="button"
					class="lightbox-nav-btn prev"
					onclick={prevLightboxPhoto}
					aria-label="Foto anterior"
				>
					<IconChevronLeft style="font-size: 26px;" />
				</button>

				<button
					type="button"
					class="lightbox-nav-btn next"
					onclick={nextLightboxPhoto}
					aria-label="Foto siguiente"
				>
					<IconChevronRight style="font-size: 26px;" />
				</button>

				<img src={currentPhoto.url} alt={currentPhoto.alt} class="lightbox-img" />

				<div class="lightbox-caption">
					<div class="caption-header">
						<h4>{currentCard.title}</h4>
						<span class="photo-counter">{lightboxState.photoIdx + 1} / {currentCard.photos.length}</span>
					</div>
					<p>{currentCard.desc}</p>
				</div>
			</div>
		</div>
	{/if}
</section>

<style>
	.gallery-section {
		background: var(--color-ecru);
		color: var(--color-plum);
		padding: var(--section-pad-lg) var(--gutter);
		position: relative;
	}

	.container {
		max-width: var(--content-max);
		margin: 0 auto;
		display: flex;
		flex-direction: column;
		align-items: center;
		gap: var(--space-10);
	}

	.section-header {
		text-align: center;
		display: flex;
		flex-direction: column;
		align-items: center;
		gap: var(--space-3);
		max-width: 720px;
	}

	.region-badge {
		display: inline-flex;
		align-items: center;
		justify-content: center;
		gap: 8px;
		margin-bottom: var(--space-2);
	}

	.badge-region {
		height: 14px;
		width: auto;
		display: block;
	}

	.badge-osorno {
		height: 19px;
		width: auto;
		display: block;
	}

	.section-title {
		font-family: var(--font-headline);
		font-size: clamp(2rem, 1.5rem + 2vw, 3.2rem);
		font-weight: 500;
		letter-spacing: 0.04em;
		color: var(--color-plum);
		margin: 0;
	}

	.section-subtitle {
		font-family: var(--font-body);
		font-size: 1.05rem;
		line-height: 1.5;
		color: var(--color-plum);
		opacity: 0.85;
		margin: 0;
	}

	.gallery-grid {
		display: grid;
		grid-template-columns: repeat(3, 1fr);
		gap: var(--space-6);
		width: 100%;
	}

	.gallery-card {
		width: 100%;
		height: 100%;
		background: var(--color-plum);
		border-radius: var(--radius-lg);
		overflow: hidden;
		display: flex;
		flex-direction: column;
		text-align: left;
		box-shadow: 0 16px 36px rgba(53, 30, 40, 0.22);
		transition: transform var(--dur-normal) var(--ease-out-expo),
			box-shadow var(--dur-normal) var(--ease-out-expo);
	}

	.gallery-card:hover {
		transform: translateY(-6px);
		box-shadow: 0 24px 50px rgba(53, 30, 40, 0.32);
	}

	.card-media {
		position: relative;
		width: 100%;
		height: 380px;
		overflow: hidden;
		cursor: pointer;
		background: #2b1821;
	}

	.gallery-img {
		position: absolute;
		inset: 0;
		width: 100%;
		height: 100%;
		object-fit: cover;
		opacity: 0;
		z-index: 0;
		pointer-events: none;
		transition: opacity 0.45s ease-in-out, transform 0.6s var(--ease-out-expo);
		transform: scale(1.02);
	}

	.gallery-img.active {
		opacity: 1;
		z-index: 1;
		pointer-events: auto;
		transform: scale(1);
	}

	.card-media:hover .gallery-img.active {
		transform: scale(1.04);
	}

	/* Subtle prev/next arrows on card hover */
	.nav-arrow {
		position: absolute;
		top: 50%;
		transform: translateY(-50%);
		width: 38px;
		height: 38px;
		border-radius: var(--radius-full);
		background: rgba(43, 24, 33, 0.78);
		backdrop-filter: blur(8px);
		-webkit-backdrop-filter: blur(8px);
		border: 1px solid rgba(225, 221, 209, 0.25);
		color: var(--color-ecru);
		display: flex;
		align-items: center;
		justify-content: center;
		cursor: pointer;
		opacity: 0;
		z-index: 4;
		transition: all var(--dur-fast) var(--ease-in-out);
		user-select: none;
	}

	.nav-arrow.prev {
		left: var(--space-3);
	}

	.nav-arrow.next {
		right: var(--space-3);
	}

	.card-media:hover .nav-arrow {
		opacity: 0.9;
	}

	.nav-arrow:hover {
		opacity: 1 !important;
		background: var(--color-lime);
		color: var(--color-plum);
		transform: translateY(-50%) scale(1.08);
	}

	.media-overlay {
		position: absolute;
		inset: 0;
		background: rgba(53, 30, 40, 0.25);
		opacity: 0;
		display: flex;
		align-items: center;
		justify-content: center;
		transition: opacity var(--dur-fast) var(--ease-in-out);
		z-index: 2;
		pointer-events: none;
	}

	.card-media:hover .media-overlay {
		opacity: 1;
	}

	.zoom-icon {
		width: 44px;
		height: 44px;
		border-radius: var(--radius-full);
		background: var(--color-lime);
		color: var(--color-plum);
		display: flex;
		align-items: center;
		justify-content: center;
		box-shadow: var(--glow-primary);
		pointer-events: auto;
		transition: transform var(--dur-fast) var(--ease-in-out);
	}

	.card-media:hover .zoom-icon:hover {
		transform: scale(1.1);
	}

	.card-footer {
		padding: var(--space-6) var(--space-6) var(--space-8) var(--space-6);
		display: flex;
		flex-direction: column;
		gap: var(--space-2);
		background: var(--color-plum);
		color: var(--color-ecru);
		flex: 1;
		position: relative;
		z-index: 5;
	}

	.card-title {
		font-family: var(--font-headline);
		font-size: 1.35rem;
		font-weight: 500;
		color: var(--color-ecru);
		letter-spacing: 0.04em;
		text-transform: uppercase;
		margin: 0;
	}

	.card-desc {
		font-family: var(--font-body);
		font-size: 0.95rem;
		line-height: 1.5;
		color: var(--color-ecru);
		opacity: 0.85;
		margin: 0;
	}

	/* Interactive Dots matching Figma design: ○ ● ● ● ● */
	.card-dots-bar {
		display: flex;
		align-items: center;
		gap: 3px;
		margin-top: var(--space-4);
	}

	.dot-btn {
		background: transparent;
		border: none;
		padding: 8px 5px;
		min-width: 24px;
		min-height: 24px;
		cursor: pointer;
		display: inline-flex;
		align-items: center;
		justify-content: center;
		touch-action: manipulation;
		transition: transform var(--dur-fast) var(--ease-in-out);
		user-select: none;
	}

	.dot-shape {
		width: 5px;
		height: 5px;
		border-radius: var(--radius-full);
		background: var(--color-ecru);
		opacity: 0.7;
		pointer-events: none;
		transition: all var(--dur-fast) var(--ease-in-out);
	}

	/* Active dot: hollow ring ○ */
	.dot-btn.active .dot-shape {
		width: 9px;
		height: 9px;
		border-radius: var(--radius-full);
		background: transparent;
		border: 1.5px solid var(--color-ecru);
		opacity: 1;
		box-shadow: 0 0 8px rgba(225, 221, 209, 0.4);
	}

	.dot-btn:hover .dot-shape {
		transform: scale(1.3);
		opacity: 1;
	}

	.dot-btn.active:hover .dot-shape {
		transform: scale(1.15);
	}

	/* Lightbox */
	.lightbox-overlay {
		position: fixed;
		inset: 0;
		z-index: 200;
		background: rgba(20, 10, 15, 0.92);
		backdrop-filter: blur(14px);
		-webkit-backdrop-filter: blur(14px);
		display: flex;
		align-items: center;
		justify-content: center;
		padding: var(--space-6);
		animation: fadeIn var(--dur-fast) var(--ease-out-expo);
	}

	.lightbox-backdrop-btn {
		position: absolute;
		inset: 0;
		width: 100%;
		height: 100%;
		background: transparent;
		border: none;
		cursor: pointer;
		padding: 0;
	}

	.lightbox-content {
		position: relative;
		max-width: 920px;
		width: 100%;
		max-height: 90vh;
		background: var(--color-plum);
		border-radius: var(--radius-lg);
		overflow: hidden;
		border: 1px solid var(--color-border-card);
		box-shadow: 0 25px 60px rgba(0, 0, 0, 0.6);
		display: flex;
		flex-direction: column;
		z-index: 10;
	}

	.lightbox-img {
		width: 100%;
		max-height: 65vh;
		object-fit: cover;
		display: block;
		background: #1d0f16;
	}

	.lightbox-nav-btn {
		position: absolute;
		top: calc(50% - 30px);
		width: 46px;
		height: 46px;
		border-radius: var(--radius-full);
		background: rgba(53, 30, 40, 0.85);
		border: 1px solid rgba(225, 221, 209, 0.3);
		color: var(--color-ecru);
		display: flex;
		align-items: center;
		justify-content: center;
		cursor: pointer;
		transition: all var(--dur-fast) var(--ease-in-out);
		z-index: 12;
	}

	.lightbox-nav-btn.prev {
		left: var(--space-4);
	}

	.lightbox-nav-btn.next {
		right: var(--space-4);
	}

	.lightbox-nav-btn:hover {
		background: var(--color-lime);
		color: var(--color-plum);
		transform: scale(1.08);
	}

	.lightbox-caption {
		padding: var(--space-6);
		background: var(--color-plum);
		color: var(--color-ecru);
		display: flex;
		flex-direction: column;
		gap: var(--space-2);
	}

	.caption-header {
		display: flex;
		align-items: center;
		justify-content: space-between;
		gap: var(--space-4);
	}

	.lightbox-caption h4 {
		font-family: var(--font-headline);
		font-size: 1.5rem;
		margin: 0;
		color: var(--color-lime);
	}

	.photo-counter {
		font-family: var(--font-body);
		font-size: var(--text-sm);
		letter-spacing: 0.1em;
		opacity: 0.75;
	}

	.lightbox-caption p {
		margin: 0;
		opacity: 0.85;
		line-height: 1.5;
	}

	.close-btn {
		position: absolute;
		top: var(--space-3);
		right: var(--space-3);
		background: rgba(53, 30, 40, 0.85);
		border: 1px solid var(--color-border-card);
		color: var(--color-ecru);
		width: 40px;
		height: 40px;
		border-radius: var(--radius-full);
		display: flex;
		align-items: center;
		justify-content: center;
		cursor: pointer;
		transition: background-color var(--dur-fast) var(--ease-in-out);
		z-index: 20;
	}

	.close-btn:hover {
		background: var(--color-lime);
		color: var(--color-plum);
	}

	@keyframes fadeIn {
		from {
			opacity: 0;
		}
		to {
			opacity: 1;
		}
	}

	@media (max-width: 960px) {
		.gallery-grid {
			grid-template-columns: 1fr;
			max-width: 500px;
			margin: 0 auto;
		}
		.card-media {
			height: 300px;
		}
		.nav-arrow {
			opacity: 0.85;
		}
		.card-footer {
			align-items: center;
			text-align: center;
		}
		.card-dots-bar {
			justify-content: center;
		}
	}
</style>
