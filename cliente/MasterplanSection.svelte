<script lang="ts">
	import imgTerreno from './assets/imgTerrenoCenital51.png';
	import imgLago from './assets/img1VolcanesLagoRupanco20211.png';
	import badgeRegion from './assets/imgGroup.svg';
	import badgeOsorno from './assets/imgGroup1.svg';
	import Icon360 from '~icons/mynaui/box';
	import IconCompass from '~icons/mynaui/compass';
	import IconSparkles from '~icons/mynaui/sparkles';


	let activeView = $state<'aerial' | 'lake'>('aerial');
	let selectedLot = $state<number | null>(7);
	let isInteractive = $state(false);

	const lots = [
		{ id: 4, name: 'Lote 04 - Mirador Volcán', area: '5.200 m²', status: 'Disponible', top: '34%', left: '28%' },
		{ id: 7, name: 'Lote 07 - Primera Línea Bosque', area: '5.050 m²', status: 'Reservado', top: '48%', left: '46%' },
		{ id: 12, name: 'Lote 12 - Orilla Río Pulleufú', area: '5.400 m²', status: 'Disponible', top: '62%', left: '68%' },
		{ id: 19, name: 'Lote 19 - Playa Lago Rupanco', area: '6.100 m²', status: 'Disponible', top: '72%', left: '32%' },
		{ id: 24, name: 'Lote 24 - Pradera Alta', area: '5.000 m²', status: 'Disponible', top: '38%', left: '74%' }
	];

	function selectLot(id: number) {
		selectedLot = id;
	}
</script>

<section class="masterplan-section" id="masterplan">
	<div class="container">
		<header class="section-header">
			<div class="region-badge" aria-label="Región de los Lagos Osorno">
				<img src={badgeRegion} alt="Región de los Lagos" class="badge-region" />
				<img src={badgeOsorno} alt="Osorno" class="badge-osorno" />
			</div>
			<h2 class="section-title">MASTERPLAN 360º</h2>
			<p class="section-subtitle">
				Explora el loteo de manera inmersiva. Navega por el terreno, revisa
				las vistas y encuentra la parcela ideal para tu futuro refugio.
			</p>
		</header>

		<div class="viewer-wrapper">
			<div class="viewer-toolbar">
				<div class="tab-group">
					<button
						type="button"
						class="tab-btn"
						class:active={activeView === 'aerial'}
						onclick={() => (activeView = 'aerial')}
					>
						<IconCompass style="font-size: 16px;" />
						<span>Vista Aérea Cenital</span>
					</button>
					<button
						type="button"
						class="tab-btn"
						class:active={activeView === 'lake'}
						onclick={() => (activeView = 'lake')}
					>
						<Icon360 style="font-size: 16px;" />
						<span>Vista 360º Lago</span>
					</button>
				</div>

				<div class="viewer-actions">
					<span class="hint-badge">
						<IconSparkles style="font-size: 14px;" />
						Haz clic en los puntos para ver parcelas
					</span>
				</div>
			</div>

			<div class="canvas-container">
				<img
					src={activeView === 'aerial' ? imgTerreno : imgLago}
					alt="Masterplan 360 interactivo del loteo Rupanco"
					class="canvas-bg"
				/>
				<div class="canvas-overlay"></div>

				{#each lots as lot}
					<button
						type="button"
						class="hotspot-pin"
						class:active={selectedLot === lot.id}
						style={`top: ${lot.top}; left: ${lot.left};`}
						onclick={() => selectLot(lot.id)}
						aria-label={`Ver detalles de ${lot.name}`}
					>
						<span class="pin-ring"></span>
						<span class="pin-core">{lot.id}</span>
					</button>
				{/each}

				{#if selectedLot !== null}
					{@const current = lots.find((l) => l.id === selectedLot)}
					{#if current}
						<div class="lot-info-card" style={`top: calc(${current.top} - 110px); left: ${current.left};`}>
							<div class="lot-header">
								<span class="lot-name">{current.name}</span>
								<span class="lot-status" class:reserved={current.status === 'Reservado'}>
									{current.status}
								</span>
							</div>
							<div class="lot-details">
								<span>Superficie: <strong>{current.area}</strong></span>
								<span>Rol Propio • Luz & Agua</span>
							</div>
							<a href="#contacto" class="lot-cta">Consultar este lote</a>
						</div>
					{/if}
				{/if}

				<div class="compass-indicator" aria-hidden="true">
					<span class="needle">N</span>
				</div>
			</div>
		</div>
	</div>
</section>

<style>
	.masterplan-section {
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
		gap: var(--space-8);
	}

	.section-header {
		text-align: center;
		display: flex;
		flex-direction: column;
		align-items: center;
		gap: var(--space-3);
		max-width: 680px;
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
		line-height: 1.55;
		color: var(--color-plum);
		opacity: 0.85;
		margin: 0;
	}

	.viewer-wrapper {
		width: 100%;
		border-radius: var(--radius-lg);
		background: var(--color-plum);
		overflow: hidden;
		box-shadow: 0 20px 50px rgba(53, 30, 40, 0.25);
		display: flex;
		flex-direction: column;
	}

	.viewer-toolbar {
		display: flex;
		align-items: center;
		justify-content: space-between;
		padding: var(--space-3) var(--space-6);
		background: rgba(53, 30, 40, 0.95);
		border-bottom: 1px solid rgba(225, 221, 209, 0.15);
	}

	.tab-group {
		display: flex;
		gap: var(--space-2);
	}

	.tab-btn {
		display: inline-flex;
		align-items: center;
		gap: var(--space-2);
		padding: var(--space-2) var(--space-4);
		border-radius: var(--radius-full);
		font-family: var(--font-body);
		font-size: var(--text-xs);
		font-weight: 600;
		border: 1px solid rgba(225, 221, 209, 0.2);
		background: transparent;
		color: var(--color-ecru);
		cursor: pointer;
		transition: all var(--dur-fast) var(--ease-in-out);
	}

	.tab-btn.active,
	.tab-btn:hover {
		background: var(--color-lime);
		color: var(--color-plum);
		border-color: var(--color-lime);
	}

	.hint-badge {
		display: inline-flex;
		align-items: center;
		gap: var(--space-2);
		font-size: var(--text-xs);
		color: var(--color-lime);
		font-weight: 500;
	}

	.canvas-container {
		position: relative;
		width: 100%;
		height: 520px;
		overflow: hidden;
		background: #8e9e85;
	}

	.canvas-bg {
		width: 100%;
		height: 100%;
		object-fit: cover;
		object-position: center;
		filter: saturate(0.95);
	}

	.canvas-overlay {
		position: absolute;
		inset: 0;
		background: radial-gradient(circle at center, transparent 40%, rgba(53, 30, 40, 0.4) 100%);
		pointer-events: none;
	}

	.hotspot-pin {
		position: absolute;
		transform: translate(-50%, -50%);
		width: 34px;
		height: 34px;
		border-radius: var(--radius-full);
		background: transparent;
		border: none;
		cursor: pointer;
		display: flex;
		align-items: center;
		justify-content: center;
		z-index: 5;
		padding: 0;
	}

	.pin-ring {
		position: absolute;
		inset: 0;
		border-radius: var(--radius-full);
		background: rgba(234, 240, 112, 0.35);
		animation: pulseRing 2s infinite ease-out;
	}

	.pin-core {
		position: relative;
		z-index: 2;
		width: 26px;
		height: 26px;
		border-radius: var(--radius-full);
		background: var(--color-lime);
		color: var(--color-plum);
		font-size: 11px;
		font-weight: 800;
		display: flex;
		align-items: center;
		justify-content: center;
		box-shadow: 0 2px 8px rgba(0, 0, 0, 0.4);
		transition: transform var(--dur-fast) var(--ease-in-out);
	}

	.hotspot-pin:hover .pin-core,
	.hotspot-pin.active .pin-core {
		transform: scale(1.2);
		background: var(--color-ecru);
		color: var(--color-plum);
	}

	@keyframes pulseRing {
		0% {
			transform: scale(0.8);
			opacity: 0.8;
		}
		100% {
			transform: scale(1.6);
			opacity: 0;
		}
	}

	.lot-info-card {
		position: absolute;
		transform: translate(-50%, 0);
		z-index: 10;
		background: rgba(53, 30, 40, 0.96);
		backdrop-filter: blur(12px);
		border: 1px solid var(--color-border-card);
		border-radius: var(--radius-md);
		padding: var(--space-4) var(--space-5);
		color: var(--color-ecru);
		min-width: 230px;
		box-shadow: 0 10px 30px rgba(0, 0, 0, 0.5);
		display: flex;
		flex-direction: column;
		gap: var(--space-2);
		animation: popIn var(--dur-fast) var(--ease-out-expo);
	}

	@keyframes popIn {
		from {
			opacity: 0;
			transform: translate(-50%, 10px);
		}
		to {
			opacity: 1;
			transform: translate(-50%, 0);
		}
	}

	.lot-header {
		display: flex;
		align-items: center;
		justify-content: space-between;
		gap: var(--space-2);
	}

	.lot-name {
		font-weight: 700;
		font-size: var(--text-sm);
		color: var(--color-lime);
	}

	.lot-status {
		font-size: 10px;
		padding: 2px 6px;
		border-radius: var(--radius-full);
		background: rgba(234, 240, 112, 0.2);
		color: var(--color-lime);
		font-weight: 700;
		text-transform: uppercase;
	}

	.lot-status.reserved {
		background: rgba(255, 92, 53, 0.2);
		color: var(--color-coral);
	}

	.lot-details {
		display: flex;
		flex-direction: column;
		font-size: var(--text-xs);
		opacity: 0.85;
		line-height: 1.4;
	}

	.lot-cta {
		margin-top: var(--space-2);
		padding: var(--space-2) var(--space-3);
		border-radius: var(--radius-full);
		background: var(--color-lime);
		color: var(--color-plum);
		font-size: var(--text-xs);
		font-weight: 700;
		text-align: center;
		text-decoration: none;
		transition: opacity var(--dur-fast) var(--ease-in-out);
	}

	.lot-cta:hover {
		opacity: 0.9;
	}

	.compass-indicator {
		position: absolute;
		bottom: var(--space-4);
		right: var(--space-4);
		width: 44px;
		height: 44px;
		border-radius: var(--radius-full);
		background: rgba(53, 30, 40, 0.85);
		border: 1px solid var(--color-border-card);
		display: flex;
		align-items: center;
		justify-content: center;
		color: var(--color-lime);
		font-weight: 800;
		font-size: var(--text-sm);
	}

	@media (max-width: 768px) {
		.canvas-container {
			height: 380px;
		}
		.viewer-toolbar {
			flex-direction: column;
			gap: var(--space-3);
			align-items: center;
			text-align: center;
		}
		.tab-group {
			justify-content: center;
			flex-wrap: wrap;
		}
		.hint-badge {
			justify-content: center;
			text-align: center;
		}
	}
</style>
