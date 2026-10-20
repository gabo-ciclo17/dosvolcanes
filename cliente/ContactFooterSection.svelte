<script lang="ts">
	import logoFooter from './assets/imgGroup3.svg';
	import monogramTop from './assets/imgGroup5.svg';
	import monogramMid from './assets/imgGroup6.svg';
	import monogramBot from './assets/imgGroup7.svg';
	import dividerLine from './assets/imgVector46.svg';
	import arrowDeco from './assets/imgArrow2.svg';
	import iconFb from './assets/imgGroup913.svg';
	import iconIg from './assets/imgGroup1333.svg';
	import iconWsp from './assets/imgGroup2.svg';
	import IconCheck from '~icons/mynaui/check';
	import IconDanger from '~icons/mynaui/danger-circle';

	let fullName = $state('');
	let rut = $state('');
	let phone = $state('');
	let email = $state('');
	let isSubmitting = $state(false);
	let isSuccess = $state(false);
	let errorMessage = $state<string | null>(null);

	async function handleSubmit(e: SubmitEvent) {
		e.preventDefault();
		if (!fullName || !phone || !email) return;

		isSubmitting = true;
		errorMessage = null;

		try {
			const res = await fetch('https://formsubmit.co/ajax/N.almarza@proyectocosmos.com', {
				method: 'POST',
				headers: {
					'Content-Type': 'application/json',
					'Accept': 'application/json'
				},
				body: JSON.stringify({
					'Nombre Completo': fullName,
					'RUT': rut || 'No indicado',
					'Teléfono': phone,
					'Correo': email,
					_subject: `Nuevo Lead Dos Volcanes Rupanco: ${fullName}`,
					_template: 'table',
					_captcha: 'false',
					_replyto: email
				})
			});

			const data = await res.json();

			if (res.ok && (data.success === 'true' || data.success === true || (data.message && data.message.includes('Activation')))) {
				isSuccess = true;
				fullName = '';
				rut = '';
				phone = '';
				email = '';
			} else {
				errorMessage = data.message || 'No fue posible enviar la información. Por favor, intenta de nuevo.';
			}
		} catch (err) {
			console.error('Error al enviar formulario:', err);
			errorMessage = 'Error de conexión al enviar el formulario. Por favor, intenta de nuevo.';
		} finally {
			isSubmitting = false;
		}
	}

	function resetSuccess() {
		isSuccess = false;
	}
</script>

<footer class="contact-footer-section" id="contacto">
	<div class="container">
		<!-- Desktop: Monogram on left, Form on right -->
		<!-- Mobile: CSS order & display:contents arranges: Form -> Divider 1 -> Logo -> Social -> Monogram -> Divider 2 -> Copyright -->
		<div class="contact-wrapper">
			<div class="brand-monogram-col">
				<div class="monogram-stack">
					<img src={monogramTop} alt="RU" class="monogram-part" />
					<img src={monogramMid} alt="PAN" class="monogram-part" />
					<img src={monogramBot} alt="CO" class="monogram-part" />
				</div>
			</div>

			<div class="contact-form-col">
				<h2 class="form-title">
					DÉJANOS TUS DATOS Y UN ASESOR ESPECIALIZADO TE CONTACTARÁ.
				</h2>

				{#if isSuccess}
					<div class="success-banner">
						<IconCheck style="font-size: 26px; flex-shrink: 0;" />
						<div class="banner-text">
							<strong>¡Solicitud enviada con éxito!</strong>
							<p>Tus datos han sido enviados correctamente. Un asesor del proyecto te contactará a la brevedad.</p>
						</div>
						<button type="button" class="banner-reset-btn" onclick={resetSuccess}>Enviar otra consulta</button>
					</div>
				{:else}
					<form class="lead-form" onsubmit={handleSubmit}>
						{#if errorMessage}
							<div class="error-banner">
								<IconDanger style="font-size: 20px; flex-shrink: 0;" />
								<span>{errorMessage}</span>
							</div>
						{/if}

						<div class="form-group full-width">
							<input
								type="text"
								name="Nombre Completo"
								bind:value={fullName}
								placeholder="NOMBRE COMPLETO"
								required
								class="input-pill"
								aria-label="Nombre completo"
								disabled={isSubmitting}
							/>
						</div>

						<div class="form-row">
							<div class="form-group half-width">
								<input
									type="text"
									name="RUT"
									bind:value={rut}
									placeholder="RUT"
									class="input-pill"
									aria-label="RUT"
									disabled={isSubmitting}
								/>
							</div>
							<div class="form-group half-width">
								<input
									type="tel"
									name="Teléfono"
									bind:value={phone}
									placeholder="TELÉFONO"
									required
									class="input-pill"
									aria-label="Teléfono"
									disabled={isSubmitting}
								/>
							</div>
						</div>

						<div class="form-group full-width">
							<input
								type="email"
								name="Correo"
								bind:value={email}
								placeholder="MAIL"
								required
								class="input-pill"
								aria-label="Correo electrónico"
								disabled={isSubmitting}
							/>
						</div>

						<div class="form-actions">
							<button type="submit" class="submit-btn" disabled={isSubmitting}>
								{#if isSubmitting}
									<span>ENVIANDO...</span>
								{:else}
									<span>SOLICITAR INFORMACIÓN</span>
								{/if}
							</button>
							<span class="privacy-note">Tus datos están seguros. No enviamos spam.</span>
						</div>
					</form>
				{/if}
			</div>
		</div>

		<!-- Divider Line 1 -->
		<div class="divider-wrapper divider-wrapper-1">
			<img src={dividerLine} alt="" aria-hidden="true" class="divider-line" />
		</div>

		<!-- Footer Bottom Elements -->
		<div class="footer-bottom-bar">
			<div class="footer-logo-block">
				<a href="#hero" aria-label="Volver arriba">
					<img src={logoFooter} alt="Dos Volcanes Logo" class="footer-logo" />
				</a>
			</div>

			<nav class="footer-nav-block" aria-label="Enlaces del pie de página">
				<ul class="footer-links">
					<li><a href="#proyecto">El proyecto</a></li>
					<li><a href="#masterplan">Masterplan 360</a></li>
					<li><a href="#ubicacion">Ubicación</a></li>
					<li><a href="#galeria">Galería</a></li>
					<li><a href="#contacto">Contacto</a></li>
				</ul>
			</nav>

			<div class="footer-arrow-block">
				<img src={arrowDeco} alt="" aria-hidden="true" class="arrow-deco" />
			</div>

			<div class="footer-social-block">
				<a href="https://facebook.com" target="_blank" rel="noopener noreferrer" class="social-icon-btn" aria-label="Facebook">
					<img src={iconFb} alt="Facebook" class="social-svg" />
				</a>
				<a href="https://instagram.com" target="_blank" rel="noopener noreferrer" class="social-icon-btn" aria-label="Instagram">
					<img src={iconIg} alt="Instagram" class="social-svg" />
				</a>
				<a href="https://whatsapp.com" target="_blank" rel="noopener noreferrer" class="social-icon-btn" aria-label="WhatsApp">
					<img src={iconWsp} alt="WhatsApp" class="social-svg" />
				</a>
			</div>
		</div>

		<!-- Divider Line 2 (Mobile only, between Monogram and Copyright) -->
		<div class="divider-wrapper divider-wrapper-2">
			<img src={dividerLine} alt="" aria-hidden="true" class="divider-line" />
		</div>

		<div class="footer-copyright">
			<p>© 2026 Dos Volcanes Rupanco.<br class="mobile-break" /> Todos los derechos reservados.</p>
		</div>
	</div>
</footer>

<style>
	.contact-footer-section {
		background: var(--color-plum);
		color: var(--color-ecru);
		padding: var(--section-pad-lg) var(--gutter) var(--space-8) var(--gutter);
		position: relative;
	}

	.container {
		max-width: var(--content-max);
		margin: 0 auto;
		display: flex;
		flex-direction: column;
		gap: var(--space-12);
	}

	.contact-wrapper {
		display: grid;
		grid-template-columns: 240px 1fr;
		gap: var(--space-16);
		align-items: center;
	}

	.brand-monogram-col {
		display: flex;
		align-items: center;
		justify-content: center;
	}

	.monogram-stack {
		display: flex;
		flex-direction: column;
		gap: var(--space-2);
		width: 146px;
	}

	.monogram-part {
		width: 100%;
		height: auto;
		display: block;
	}

	.contact-form-col {
		display: flex;
		flex-direction: column;
		gap: var(--space-6);
		max-width: 680px;
	}

	.form-title {
		font-family: var(--font-headline);
		font-size: clamp(1.4rem, 1.1rem + 1vw, 1.85rem);
		font-weight: 700;
		line-height: 1.25;
		color: var(--color-ecru);
		letter-spacing: 0.04em;
		margin: 0;
	}

	.lead-form {
		display: flex;
		flex-direction: column;
		gap: var(--space-3);
	}

	.form-row {
		display: flex;
		gap: var(--space-3);
	}

	.form-group {
		width: 100%;
	}

	.half-width {
		flex: 1;
	}

	.input-pill {
		width: 100%;
		box-sizing: border-box;
		height: 48px;
		padding: 0 var(--space-6);
		border-radius: var(--radius-full);
		border: 1px solid var(--color-ecru);
		background: transparent;
		color: var(--color-ecru);
		font-family: var(--font-body);
		font-size: var(--text-sm);
		letter-spacing: 0.08em;
		text-transform: uppercase;
		outline: none;
		transition: border-color var(--dur-fast) var(--ease-in-out),
			box-shadow var(--dur-fast) var(--ease-in-out);
	}

	.input-pill::placeholder {
		color: rgba(225, 221, 209, 0.7);
	}

	.input-pill:focus {
		border-color: var(--color-lime);
		box-shadow: 0 0 12px rgba(234, 240, 112, 0.3);
	}

	.form-actions {
		display: flex;
		align-items: center;
		gap: var(--space-4);
		margin-top: var(--space-3);
		flex-wrap: wrap;
	}

	.submit-btn {
		display: inline-flex;
		align-items: center;
		justify-content: center;
		height: 48px;
		padding: 0 var(--space-8);
		border-radius: var(--radius-full);
		border: none;
		background: var(--color-ecru);
		color: var(--color-plum);
		font-family: var(--font-body);
		font-size: var(--text-sm);
		font-weight: 700;
		letter-spacing: 0.1em;
		text-transform: uppercase;
		cursor: pointer;
		transition: all var(--dur-fast) var(--ease-in-out);
	}

	.submit-btn:hover:not(:disabled) {
		background: var(--color-lime);
		color: var(--color-plum);
		transform: translateY(-2px);
		box-shadow: var(--glow-primary);
	}

	.submit-btn:disabled {
		opacity: 0.7;
		cursor: not-allowed;
	}

	.privacy-note {
		font-family: var(--font-body);
		font-size: var(--text-xs);
		color: rgba(225, 221, 209, 0.75);
	}

	.error-banner {
		display: flex;
		align-items: center;
		gap: var(--space-3);
		background: rgba(255, 92, 53, 0.15);
		border: 1px solid var(--color-coral);
		color: #ff9b80;
		padding: var(--space-3) var(--space-5);
		border-radius: var(--radius-md);
		font-size: var(--text-xs);
		animation: fadeIn var(--dur-fast) ease-out;
	}

	.success-banner {
		display: flex;
		align-items: center;
		gap: var(--space-4);
		background: rgba(234, 240, 112, 0.15);
		border: 1px solid var(--color-lime);
		color: var(--color-lime);
		padding: var(--space-5) var(--space-6);
		border-radius: var(--radius-md);
		animation: fadeIn var(--dur-fast) ease-out;
		flex-wrap: wrap;
	}

	.banner-text {
		display: flex;
		flex-direction: column;
		gap: 2px;
		flex: 1;
		min-width: 200px;
	}

	.banner-text strong {
		color: var(--color-lime);
		font-size: var(--text-base);
	}

	.banner-text p {
		margin: 0;
		font-size: var(--text-xs);
		color: var(--color-ecru);
		opacity: 0.9;
		line-height: 1.4;
	}

	.banner-reset-btn {
		background: transparent;
		border: 1px solid var(--color-lime);
		color: var(--color-lime);
		padding: 6px 14px;
		border-radius: var(--radius-full);
		font-family: var(--font-body);
		font-size: 11px;
		font-weight: 700;
		letter-spacing: 0.05em;
		text-transform: uppercase;
		cursor: pointer;
		transition: all var(--dur-fast) var(--ease-in-out);
	}

	.banner-reset-btn:hover {
		background: var(--color-lime);
		color: var(--color-plum);
	}

	@keyframes fadeIn {
		from { opacity: 0; transform: translateY(-4px); }
		to { opacity: 1; transform: translateY(0); }
	}

	.divider-wrapper {
		width: 100%;
		opacity: 0.35;
	}

	.divider-line {
		width: 100%;
		height: 1px;
		display: block;
	}

	/* Footer Bar */
	.footer-bottom-bar {
		display: flex;
		align-items: center;
		justify-content: space-between;
		gap: var(--space-8);
		flex-wrap: wrap;
		padding-top: var(--space-2);
	}

	.footer-logo {
		height: 32px;
		width: auto;
		display: block;
	}

	.footer-links {
		list-style: none;
		margin: 0;
		padding: 0;
		display: flex;
		flex-direction: column;
		gap: var(--space-1);
	}

	.footer-links a {
		font-family: var(--font-body);
		font-size: var(--text-sm);
		color: var(--color-ecru);
		text-decoration: none;
		opacity: 0.85;
		transition: opacity var(--dur-fast) var(--ease-in-out), color var(--dur-fast) var(--ease-in-out);
	}

	.footer-links a:hover {
		opacity: 1;
		color: var(--color-lime);
	}

	.footer-arrow-block {
		flex: 1;
		display: flex;
		align-items: center;
		justify-content: center;
		max-width: 280px;
	}

	.arrow-deco {
		width: 100%;
		height: auto;
		display: block;
	}

	.footer-social-block {
		display: flex;
		align-items: center;
		gap: var(--space-4);
	}

	.social-icon-btn {
		display: flex;
		align-items: center;
		justify-content: center;
		width: 36px;
		height: 36px;
		border-radius: var(--radius-full);
		transition: transform var(--dur-fast) var(--ease-in-out);
	}

	.social-icon-btn:hover {
		transform: scale(1.15);
	}

	.social-svg {
		height: 28px;
		width: auto;
		display: block;
	}

	.footer-copyright {
		text-align: center;
		font-family: var(--font-body);
		font-size: var(--text-xs);
		color: rgba(225, 221, 209, 0.6);
		margin-top: var(--space-4);
	}

	.divider-wrapper-2 {
		display: none;
	}

	.mobile-break {
		display: none;
	}

	@media (max-width: 900px) {
		.contact-footer-section {
			padding: var(--section-pad-md) var(--space-6) var(--space-10) var(--space-6);
		}

		.container {
			display: flex;
			flex-direction: column;
			align-items: center;
			gap: 0;
			max-width: 340px;
			margin: 0 auto;
			width: 100%;
		}

		.contact-wrapper {
			display: contents;
		}

		.footer-bottom-bar {
			display: contents;
		}

		.contact-form-col {
			order: 1;
			display: flex;
			flex-direction: column;
			align-items: center;
			width: 100%;
			max-width: 326px;
			margin: 0 auto;
		}

		.form-title {
			max-width: 317px;
			margin: 0 auto var(--space-6) auto;
			text-align: center;
			font-family: var(--font-headline);
			font-size: clamp(1.4rem, 1.25rem + 1vw, 1.7rem);
			line-height: 1.22;
			letter-spacing: 0.04em;
		}

		.lead-form {
			display: flex;
			flex-direction: column;
			gap: 12px;
			width: 100%;
		}

		.form-row {
			display: flex;
			flex-direction: column;
			gap: 12px;
			width: 100%;
		}

		.form-group {
			width: 100%;
		}

		.input-pill {
			width: 100%;
			height: 46px;
			padding: 0 24px;
			border-radius: var(--radius-full);
			border: 1px solid rgba(225, 221, 209, 0.45);
			background: transparent;
			color: var(--color-ecru);
			font-family: var(--font-headline);
			font-size: var(--text-sm);
			letter-spacing: 0.08em;
			text-transform: uppercase;
			outline: none;
		}

		.input-pill::placeholder {
			color: rgba(225, 221, 209, 0.7);
			font-family: var(--font-headline);
			letter-spacing: 0.08em;
		}

		.form-actions {
			display: flex;
			flex-direction: column;
			align-items: center;
			gap: var(--space-4);
			width: 100%;
			margin-top: var(--space-2);
		}

		.submit-btn {
			width: 100%;
			height: 46px;
			padding: 0 24px;
			border-radius: var(--radius-full);
			background: var(--color-ecru);
			color: var(--color-plum);
			font-family: var(--font-headline);
			font-size: 0.95rem;
			font-weight: 600;
			letter-spacing: 0.06em;
			text-transform: uppercase;
			border: none;
			margin: 0 auto;
			box-shadow: 0 4px 14px rgba(0, 0, 0, 0.18);
		}

		.submit-btn:hover:not(:disabled) {
			background: var(--color-lime);
			color: var(--color-plum);
		}

		.privacy-note {
			font-family: var(--font-headline);
			font-size: 0.85rem;
			color: rgba(225, 221, 209, 0.75);
			text-align: center;
			margin-top: 0;
		}

		.divider-wrapper-1 {
			order: 2;
			display: block;
			width: 100%;
			max-width: 326px;
			margin: var(--space-8) auto var(--space-8) auto;
			opacity: 0.35;
		}

		.footer-logo-block {
			order: 3;
			display: flex;
			justify-content: center;
			width: 100%;
			margin: 0 auto var(--space-5) auto;
		}

		.footer-logo {
			width: 220px;
			max-width: 80%;
			height: auto;
			display: block;
			margin: 0 auto;
		}

		.footer-social-block {
			order: 4;
			display: flex;
			align-items: center;
			justify-content: center;
			gap: var(--space-6);
			width: 100%;
			margin: 0 auto var(--space-10) auto;
		}

		.social-icon-btn {
			width: 36px;
			height: 36px;
			display: flex;
			align-items: center;
			justify-content: center;
		}

		.social-svg {
			height: 30px;
			width: auto;
		}

		.brand-monogram-col {
			order: 5;
			display: flex;
			justify-content: center;
			width: 100%;
			margin: 0 auto var(--space-6) auto;
		}

		.monogram-stack {
			width: 146px;
			display: flex;
			flex-direction: column;
			gap: var(--space-2);
			align-items: center;
		}

		.monogram-part {
			width: 100%;
			height: auto;
		}

		.divider-wrapper-2 {
			order: 6;
			display: block;
			width: 100%;
			max-width: 326px;
			margin: 0 auto var(--space-8) auto;
			opacity: 0.35;
		}

		.footer-copyright {
			order: 7;
			text-align: center;
			width: 100%;
			margin: 0 auto;
			font-family: var(--font-headline);
			font-size: 0.85rem;
			line-height: 1.5;
			color: rgba(225, 221, 209, 0.7);
		}

		.mobile-break {
			display: block;
		}

		.footer-nav-block {
			display: none;
		}

		.footer-arrow-block {
			display: none;
		}
	}
</style>
