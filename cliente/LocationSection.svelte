<script lang="ts">
	import badgeImg from './assets/imgCapa2.svg';
	import iconPlane from './assets/imgCapa3.svg';
	import iconCar from './assets/imgCapa5.svg';
	import iconBoat from './assets/imgCapa4.svg';
	import iconCircle from './assets/imgGroup1348.svg';
	import imgMapSatellite from './assets/imgSunlitForestPathWithLushGreenMoss1.png';
	import IconMapPin from '~icons/mynaui/map-pin';
	import IconNavigation from '~icons/mynaui/navigation';

	interface LocationCard {
		title: string;
		desc: string;
		icon: string;
		alt: string;
	}

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
				Explora el loteo de manera inmersiva. Navega por el terreno, revisa las
				vistas y encuentra la parcela ideal para tu futuro refugio.
			</p>
		</header>

		<!-- Interactive Map Showcase -->
		<div class="map-showcase">
			<div class="map-canvas">
				<img src={imgMapSatellite} alt="Ubicación geográfica Lago Rupanco" class="map-bg" />
				<div class="map-overlay"></div>

				<!-- Visual Map Highlights -->
				<div class="map-pin-point" style="top: 48%; left: 52%;">
					<div class="pin-radar"></div>
					<div class="pin-marker">
						<IconMapPin style="font-size: 18px;" />
					</div>
					<div class="pin-tooltip">
						<strong>Dos Volcanes Rupanco</strong>
						<span>Sector El Desagüe / Río Pulleufú</span>
					</div>
				</div>

				<div class="map-poi" style="top: 25%; left: 24%;">
					<span class="poi-dot"></span>
					<span class="poi-label">Aeropuerto Osorno (55 min)</span>
				</div>

				<div class="map-poi" style="top: 36%; left: 40%;">
					<span class="poi-dot"></span>
					<span class="poi-label">Entrelagos (20 min)</span>
				</div>

				<div class="map-poi" style="top: 40%; left: 75%;">
					<span class="poi-dot"></span>
					<span class="poi-label">Termas Puyehue (30 min)</span>
				</div>

				<div class="map-poi" style="top: 68%; left: 78%;">
					<span class="poi-dot"></span>
					<span class="poi-label">Antillanca Ski (45 min)</span>
				</div>

				<div class="map-route-indicator">
					<IconNavigation style="font-size: 14px;" />
					<span>Ruta asfaltada hasta acceso principal</span>
				</div>
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
		overflow: hidden;
		box-shadow: 0 20px 45px rgba(53, 30, 40, 0.25);
		border: 2px solid rgba(53, 30, 40, 0.15);
	}

	.map-canvas {
		position: relative;
		width: 100%;
		height: 440px;
		background: #8e9e85;
		overflow: hidden;
	}

	.map-bg {
		width: 100%;
		height: 100%;
		object-fit: cover;
		filter: saturate(0.85) contrast(1.05);
	}

	.map-overlay {
		position: absolute;
		inset: 0;
		background: linear-gradient(180deg, rgba(53, 30, 40, 0.3) 0%, rgba(255, 92, 53, 0.2) 100%);
	}

	.map-pin-point {
		position: absolute;
		transform: translate(-50%, -50%);
		display: flex;
		flex-direction: column;
		align-items: center;
		z-index: 10;
	}

	.pin-radar {
		position: absolute;
		top: 50%;
		left: 50%;
		transform: translate(-50%, -50%);
		width: 50px;
		height: 50px;
		border-radius: var(--radius-full);
		background: rgba(234, 240, 112, 0.35);
		animation: radarPulse 2s infinite ease-out;
	}

	.pin-marker {
		position: relative;
		z-index: 2;
		width: 36px;
		height: 36px;
		border-radius: var(--radius-full);
		background: var(--color-lime);
		color: var(--color-plum);
		display: flex;
		align-items: center;
		justify-content: center;
		box-shadow: 0 4px 12px rgba(0, 0, 0, 0.4);
	}

	.pin-tooltip {
		margin-top: var(--space-2);
		background: var(--color-plum);
		color: var(--color-ecru);
		padding: var(--space-2) var(--space-3);
		border-radius: var(--radius-sm);
		font-size: var(--text-xs);
		display: flex;
		flex-direction: column;
		align-items: center;
		white-space: nowrap;
		box-shadow: 0 6px 16px rgba(0, 0, 0, 0.4);
	}

	.pin-tooltip strong {
		color: var(--color-lime);
	}

	@keyframes radarPulse {
		0% {
			transform: translate(-50%, -50%) scale(0.6);
			opacity: 0.9;
		}
		100% {
			transform: translate(-50%, -50%) scale(1.8);
			opacity: 0;
		}
	}

	.map-poi {
		position: absolute;
		display: flex;
		align-items: center;
		gap: var(--space-2);
		background: rgba(53, 30, 40, 0.85);
		backdrop-filter: blur(8px);
		color: var(--color-ecru);
		padding: 4px 10px;
		border-radius: var(--radius-full);
		font-size: 11px;
		font-weight: 600;
		box-shadow: 0 4px 12px rgba(0, 0, 0, 0.25);
	}

	.poi-dot {
		width: 6px;
		height: 6px;
		border-radius: var(--radius-full);
		background: var(--color-lime);
	}

	.map-route-indicator {
		position: absolute;
		bottom: var(--space-4);
		left: var(--space-4);
		display: inline-flex;
		align-items: center;
		gap: var(--space-2);
		background: rgba(53, 30, 40, 0.9);
		color: var(--color-lime);
		padding: var(--space-2) var(--space-4);
		border-radius: var(--radius-full);
		font-size: var(--text-xs);
		font-weight: 600;
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
		.map-canvas {
			height: 340px;
		}
	}
</style>
