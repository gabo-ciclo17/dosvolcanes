<script lang="ts">
	import badgeImg from './assets/imgCapa2.svg';
	import iconPlane from './assets/imgCapa3.svg';
	import iconCar from './assets/imgCapa5.svg';
	import iconBoat from './assets/imgCapa4.svg';
	import iconCircle from './assets/imgGroup1348.svg';
	import IconMap from '~icons/mynaui/map';
	import IconExternal from '~icons/mynaui/external-link';

	interface LocationCard {
		title: string;
		desc: string;
		icon: string;
		alt: string;
	}

	let isMapLoaded = $state(false);

	const cards: LocationCard[] = [
		{
			title: 'AEROPUERTO OSORNO',
			desc: 'Un espacio único de naturaleza virgen, bosques nativos y paisajes inigualables a solo 55 min en ruta asfaltada.',
			icon: iconPlane,
			alt: 'Icono de conectividad aérea con Aeropuerto de Osorno'
		},
		{
			title: 'CENTROS URBANOS',
			desc: 'Entrelagos: 20 min, Termas de Puyehue: 30 min, Centro Ski Antillanca: 45 min, Bariloche (ARG): 3 hrs.',
			icon: iconCar,
			alt: 'Icono de centros urbanos y servicios cercanos'
		},
		{
			title: 'ATRACCIONES NÁUTICAS',
			desc: 'Saltos del Calzoncillo: 5 min en lancha. Río Pulleufú: 10 min en lancha. Playa de aguas cristalinas.',
			icon: iconBoat,
			alt: 'Icono de navegación y actividades náuticas'
		}
	];
</script>

<section class="location-section" id="ubicacion">
	<div class="container">
		<header class="section-header">
			<div class="badge-wrapper">
				<img src={badgeImg} alt="Región de los Lagos Osorno" class="badge-icon" />
			</div>
			<h2 class="section-title">UN PARAÍSO AISLADO, PERO CONECTADO</h2>
			<p class="section-subtitle">
				Ubicación estratégica en la ribera sur del Lago Rupanco con accesibilidad directa por ruta asfaltada, conectando con aeropuertos, termas y centros turísticos de la X Región.
			</p>
		</header>

		<!-- Interactive Map Showcase -->
		<div class="map-showcase">
			<div class="map-toolbar">
				<div class="map-status-badge">
					<IconMap style="font-size: 16px;" />
					<span>Google Maps</span>
				</div>

				<div class="map-toolbar-actions">
					<a
						href="https://www.google.com/maps/search/?api=1&query=Lago+Rupanco"
						target="_blank"
						rel="noopener noreferrer"
						class="open-map-link"
						title="Abrir ubicación en Google Maps"
					>
						<span>Ver en Google Maps</span>
						<IconExternal style="font-size: 14px;" />
					</a>
				</div>
			</div>

			<!-- Google Maps Iframe Container -->
			<div class="map-frame-container">
				{#if !isMapLoaded}
					<div class="map-loader" aria-live="polite">
						<div class="loader-spinner"></div>
						<p class="loader-label">Cargando Google Maps...</p>
					</div>
				{/if}
				<iframe
					src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d193204.55869340888!2d-72.5990743622675!3d-40.831890204386!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x96170ec3866f48df%3A0x2dfc212cb3d31e25!2sLago%20Rupanco!5e0!3m2!1ses!2scl!4v1792419191743!5m2!1ses!2scl"
					width="100%"
					height="100%"
					style="border:0;"
					allowfullscreen
					loading="lazy"
					referrerpolicy="strict-origin-when-cross-origin"
					title="Ubicación Lago Rupanco en Google Maps"
					class="google-map-iframe"
					onload={() => (isMapLoaded = true)}
				></iframe>
			</div>
		</div>

		<!-- 3 Location Cards -->
		<div class="cards-grid">
			{#each cards as item}
				<article class="location-card">
					<div class="icon-header">
						<div class="icon-circle-bg">
							<img src={iconCircle} alt="" aria-hidden="true" class="circle-svg" />
							<img src={item.icon} alt={item.alt} class="category-icon" />
						</div>
					</div>
					<div class="card-content">
						<h3 class="card-title">{item.title}</h3>
						<p class="card-desc">{item.desc}</p>
					</div>
				</article>
			{/each}
		</div>
	</div>
</section>

<style>
	.location-section {
		background: var(--color-coral);
		color: var(--color-plum);
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
		gap: var(--space-10);
	}

	.section-header {
		text-align: center;
		display: flex;
		flex-direction: column;
		align-items: center;
		gap: var(--space-4);
		max-width: 820px;
	}

	.badge-wrapper {
		display: flex;
		align-items: center;
		justify-content: center;
	}

	.badge-icon {
		height: 20px;
		width: auto;
		filter: brightness(0.2);
	}

	.section-title {
		font-family: var(--font-headline);
		font-size: clamp(2rem, 1.5rem + 2.2vw, 3.2rem);
		font-weight: 500;
		line-height: 1.15;
		color: var(--color-plum);
		text-transform: uppercase;
		letter-spacing: 0.04em;
		margin: 0;
	}

	.section-subtitle {
		font-family: var(--font-body);
		font-size: 1.05rem;
		line-height: 1.55;
		color: var(--color-plum);
		opacity: 0.9;
		margin: 0;
		max-width: 680px;
	}

	.map-showcase {
		width: 100%;
		border-radius: var(--radius-lg);
		background: var(--color-plum);
		overflow: hidden;
		box-shadow: 0 20px 45px rgba(53, 30, 40, 0.25);
		border: 1px solid rgba(53, 30, 40, 0.25);
		display: flex;
		flex-direction: column;
	}

	.map-toolbar {
		display: flex;
		align-items: center;
		justify-content: space-between;
		padding: var(--space-3) var(--space-6);
		background: rgba(53, 30, 40, 0.96);
		border-bottom: 1px solid rgba(225, 221, 209, 0.15);
	}

	.map-status-badge {
		display: inline-flex;
		align-items: center;
		gap: var(--space-2);
		padding: var(--space-2) var(--space-4);
		border-radius: var(--radius-full);
		font-family: var(--font-body);
		font-size: var(--text-xs);
		font-weight: 700;
		background: var(--color-lime);
		color: var(--color-plum);
		letter-spacing: 0.04em;
	}

	.open-map-link {
		display: inline-flex;
		align-items: center;
		gap: 6px;
		padding: var(--space-2) var(--space-4);
		border-radius: var(--radius-full);
		font-family: var(--font-body);
		font-size: var(--text-xs);
		font-weight: 600;
		background: rgba(234, 240, 112, 0.15);
		color: var(--color-lime);
		border: 1px solid rgba(234, 240, 112, 0.35);
		text-decoration: none;
		transition: all var(--dur-fast) var(--ease-in-out);
	}

	.open-map-link:hover {
		background: var(--color-lime);
		color: var(--color-plum);
		border-color: var(--color-lime);
	}

	.map-frame-container {
		position: relative;
		width: 100%;
		height: clamp(440px, 55vh, 560px);
		background: #25151e;
		overflow: hidden;
	}

	.google-map-iframe {
		width: 100%;
		height: 100%;
		border: 0;
		display: block;
	}

	.map-loader {
		position: absolute;
		inset: 0;
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		gap: var(--space-3);
		background: #25151e;
		color: var(--color-ecru);
		z-index: 2;
	}

	.loader-spinner {
		width: 36px;
		height: 36px;
		border-radius: 50%;
		border: 3px solid rgba(234, 240, 112, 0.2);
		border-top-color: var(--color-lime);
		animation: spinMapLoader 0.9s linear infinite;
	}

	.loader-label {
		font-size: var(--text-xs);
		color: var(--color-ecru);
		opacity: 0.85;
		margin: 0;
		font-family: var(--font-body);
		letter-spacing: 0.05em;
	}

	@keyframes spinMapLoader {
		to {
			transform: rotate(360deg);
		}
	}

	.cards-grid {
		display: grid;
		grid-template-columns: repeat(3, 1fr);
		gap: var(--space-6);
		width: 100%;
	}

	.location-card {
		background: var(--color-ecru);
		border-radius: var(--radius-lg);
		padding: var(--space-8) var(--space-6) var(--space-10) var(--space-6);
		display: flex;
		flex-direction: column;
		align-items: center;
		text-align: center;
		box-shadow: 0 14px 35px rgba(53, 30, 40, 0.2);
		transition: transform var(--dur-normal) var(--ease-out-expo),
			box-shadow var(--dur-normal) var(--ease-out-expo);
	}

	.location-card:hover {
		transform: translateY(-6px);
		box-shadow: 0 20px 45px rgba(53, 30, 40, 0.3);
	}

	.icon-header {
		margin-bottom: var(--space-6);
	}

	.icon-circle-bg {
		position: relative;
		width: 72px;
		height: 72px;
		display: flex;
		align-items: center;
		justify-content: center;
	}

	.circle-svg {
		position: absolute;
		inset: 0;
		width: 100%;
		height: 100%;
	}

	.category-icon {
		position: relative;
		z-index: 2;
		max-width: 44px;
		max-height: 32px;
		object-fit: contain;
	}

	.card-content {
		display: flex;
		flex-direction: column;
		gap: var(--space-2);
	}

	.card-title {
		font-family: var(--font-headline);
		font-size: 1.35rem;
		font-weight: 700;
		color: var(--color-plum);
		text-transform: uppercase;
		letter-spacing: 0.02em;
		margin: 0;
	}

	.card-desc {
		font-family: var(--font-body);
		font-size: 0.95rem;
		line-height: 1.5;
		color: var(--color-plum);
		opacity: 0.85;
		margin: 0;
	}

	@media (max-width: 960px) {
		.cards-grid {
			grid-template-columns: 1fr;
		}
		.map-frame-container {
			height: 380px;
		}
		.map-toolbar {
			flex-direction: column;
			gap: var(--space-3);
			align-items: center;
			text-align: center;
		}
		.map-toolbar-actions {
			justify-content: center;
		}
	}
</style>
