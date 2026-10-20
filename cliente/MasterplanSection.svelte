<script lang="ts">
	import badgeRegion from './assets/imgGroup.svg';
	import badgeOsorno from './assets/imgGroup1.svg';
	import Icon360 from '~icons/mynaui/box';
	import IconSparkles from '~icons/mynaui/sparkles';
	import IconExternal from '~icons/mynaui/external-link';

	let isTourLoaded = $state(false);
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
				Explora el loteo de manera inmersiva. Navega en 360º por el terreno, revisa
				las vistas y encuentra la parcela ideal para tu futuro refugio.
			</p>
		</header>

		<div class="viewer-wrapper">
			<div class="viewer-toolbar">
				<div class="tour-status-badge">
					<Icon360 style="font-size: 16px;" />
					<span>Tour Virtual 360º</span>
					<span class="live-dot" aria-label="En vivo"></span>
				</div>

				<div class="viewer-actions">
					<span class="hint-badge desktop-only">
						<IconSparkles style="font-size: 14px;" />
						Arrastra para rotar en 360º
					</span>
					<a
						href="https://www.lanube360.com/dosvolcanes/"
						target="_blank"
						rel="noopener noreferrer"
						class="open-link"
						title="Abrir Tour 360 en pantalla completa"
					>
						<span>Pantalla Completa</span>
						<IconExternal style="font-size: 14px;" />
					</a>
				</div>
			</div>

			<!-- Tour 360 View (LaNube360) -->
			<div class="tour-frame-container">
				{#if !isTourLoaded}
					<div class="frame-loader" aria-live="polite">
						<div class="loader-spinner"></div>
						<p class="loader-label">Cargando Tour Virtual 360º...</p>
					</div>
				{/if}
				<iframe
					src="https://www.lanube360.com/dosvolcanes/"
					title="Tour Virtual 360º Dos Volcanes Rupanco"
					class="tour-iframe"
					allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; xr-spatial-tracking; fullscreen"
					allowfullscreen
					loading="lazy"
					referrerpolicy="no-referrer-when-downgrade"
					onload={() => (isTourLoaded = true)}
				></iframe>
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
		border: 1px solid rgba(53, 30, 40, 0.15);
	}

	.viewer-toolbar {
		display: flex;
		align-items: center;
		justify-content: space-between;
		padding: var(--space-3) var(--space-6);
		background: rgba(53, 30, 40, 0.95);
		border-bottom: 1px solid rgba(225, 221, 209, 0.15);
	}

	.tour-status-badge {
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

	.live-dot {
		width: 7px;
		height: 7px;
		border-radius: var(--radius-full);
		background: var(--color-plum);
		box-shadow: 0 0 6px var(--color-plum);
		animation: pulseDot 1.6s infinite;
	}

	@keyframes pulseDot {
		0%, 100% {
			opacity: 1;
			transform: scale(1);
		}
		50% {
			opacity: 0.35;
			transform: scale(0.75);
		}
	}

	.hint-badge {
		display: inline-flex;
		align-items: center;
		gap: var(--space-2);
		font-size: var(--text-xs);
		color: var(--color-lime);
		font-weight: 500;
	}

	.viewer-actions {
		display: flex;
		align-items: center;
		gap: var(--space-4);
	}

	.open-link {
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

	.open-link:hover {
		background: var(--color-lime);
		color: var(--color-plum);
		border-color: var(--color-lime);
	}

	.tour-frame-container {
		position: relative;
		width: 100%;
		height: clamp(520px, 68vh, 720px);
		background: #1e1117;
		overflow: hidden;
	}

	.tour-iframe {
		width: 100%;
		height: 100%;
		border: 0;
		display: block;
	}

	.frame-loader {
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
		width: 38px;
		height: 38px;
		border-radius: 50%;
		border: 3px solid rgba(234, 240, 112, 0.2);
		border-top-color: var(--color-lime);
		animation: spinLoader 0.9s linear infinite;
	}

	.loader-label {
		font-size: var(--text-xs);
		color: var(--color-ecru);
		opacity: 0.85;
		margin: 0;
		font-family: var(--font-body);
		letter-spacing: 0.05em;
	}

	@keyframes spinLoader {
		to {
			transform: rotate(360deg);
		}
	}

	@media (max-width: 768px) {
		.tour-frame-container {
			height: 440px;
		}
		.desktop-only {
			display: none;
		}
		.viewer-toolbar {
			flex-direction: column;
			gap: var(--space-3);
			align-items: center;
			text-align: center;
		}
		.viewer-actions {
			justify-content: center;
			flex-wrap: wrap;
		}
		.hint-badge {
			justify-content: center;
			text-align: center;
		}
	}
</style>
