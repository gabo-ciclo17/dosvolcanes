<script lang="ts">
	import logoImg from './assets/imgModoDeAislamiento1.svg';
	import IconMenu from '~icons/mynaui/menu';
	import IconX from '~icons/mynaui/x';

	let isScrolled = $state(false);
	let mobileMenuOpen = $state(false);

	function onWindowScroll() {
		if (typeof window !== 'undefined') {
			isScrolled = window.scrollY > 40;
		}
	}

	function toggleMobileMenu() {
		mobileMenuOpen = !mobileMenuOpen;
	}

	function closeMenu() {
		mobileMenuOpen = false;
	}
</script>

<svelte:window onscroll={onWindowScroll} />

<header class="navbar-wrapper" class:scrolled={isScrolled}>
	<div class="navbar-inner">
		<a href="#hero" class="brand-link" aria-label="Dos Volcanes Rupanco - Inicio">
			<img src={logoImg} alt="Dos Volcanes Logo" class="brand-logo" width="167" height="24" />
		</a>

		<nav class="desktop-nav" aria-label="Navegación principal">
			<ul class="nav-list">
				<li><a href="#proyecto" class="nav-link">EL PROYECTO</a></li>
				<li><a href="#masterplan" class="nav-link">MASTERPLAN 360</a></li>
				<li><a href="#ubicacion" class="nav-link">UBICACIÓN</a></li>
				<li><a href="#galeria" class="nav-link">GALERÍA</a></li>
				<li><a href="#contacto" class="nav-link">CONTACTO</a></li>
			</ul>
		</nav>

		<button
			type="button"
			class="mobile-toggle"
			onclick={toggleMobileMenu}
			aria-expanded={mobileMenuOpen}
			aria-label="Abrir menú móvil"
		>
			{#if mobileMenuOpen}
				<IconX style="font-size: 24px;" />
			{:else}
				<IconMenu style="font-size: 24px;" />
			{/if}
		</button>
	</div>

	{#if mobileMenuOpen}
		<div class="mobile-drawer">
			<ul class="mobile-nav-list">
				<li><a href="#proyecto" onclick={closeMenu} class="mobile-link">EL PROYECTO</a></li>
				<li><a href="#masterplan" onclick={closeMenu} class="mobile-link">MASTERPLAN 360</a></li>
				<li><a href="#ubicacion" onclick={closeMenu} class="mobile-link">UBICACIÓN</a></li>
				<li><a href="#galeria" onclick={closeMenu} class="mobile-link">GALERÍA</a></li>
				<li><a href="#contacto" onclick={closeMenu} class="mobile-link">CONTACTO</a></li>
			</ul>
		</div>
	{/if}
</header>

<style>
	.navbar-wrapper {
		position: fixed;
		top: 0;
		left: 0;
		width: 100%;
		z-index: 100;
		transition: background-color var(--dur-normal) var(--ease-in-out),
			backdrop-filter var(--dur-normal) var(--ease-in-out),
			border-color var(--dur-normal) var(--ease-in-out);
		background: transparent;
		border-bottom: 1px solid transparent;
	}

	.navbar-wrapper.scrolled {
		background: rgba(53, 30, 40, 0.9);
		backdrop-filter: blur(16px);
		-webkit-backdrop-filter: blur(16px);
		border-bottom: 1px solid var(--color-border-card);
	}

	.navbar-inner {
		max-width: var(--content-max);
		margin: 0 auto;
		padding: var(--space-6) var(--gutter);
		display: flex;
		align-items: center;
		justify-content: space-between;
		height: var(--navbar-height);
	}

	.brand-link {
		display: flex;
		align-items: center;
		text-decoration: none;
	}

	.brand-logo {
		height: 24px;
		width: auto;
		display: block;
		transition: transform var(--dur-fast) var(--ease-in-out), filter var(--dur-fast) var(--ease-in-out);
	}

	.brand-link:hover .brand-logo {
		filter: drop-shadow(0 0 10px rgba(234, 240, 112, 0.5));
	}

	.desktop-nav {
		display: flex;
		align-items: center;
	}

	.nav-list {
		display: flex;
		align-items: center;
		gap: var(--space-8);
		list-style: none;
		margin: 0;
		padding: 0;
	}

	.nav-link {
		font-family: var(--font-headline);
		font-size: var(--text-sm);
		font-weight: 500;
		letter-spacing: 0.1em;
		text-transform: uppercase;
		color: var(--color-lime);
		text-decoration: none;
		position: relative;
		transition: color var(--dur-fast) var(--ease-in-out), opacity var(--dur-fast) var(--ease-in-out);
		opacity: 0.95;
	}

	.nav-link:hover {
		color: var(--color-lime);
		opacity: 1;
		text-shadow: 0 0 12px rgba(234, 240, 112, 0.5);
	}

	.mobile-toggle {
		display: none;
		background: none;
		border: none;
		color: var(--color-lime);
		cursor: pointer;
		padding: var(--space-2);
	}

	.mobile-drawer {
		display: flex;
		flex-direction: column;
		background: var(--color-plum);
		border-bottom: 1px solid var(--color-border-card);
		padding: var(--space-6) var(--gutter);
		gap: var(--space-4);
		align-items: center;
		text-align: center;
	}

	.mobile-nav-list {
		list-style: none;
		margin: 0;
		padding: 0;
		display: flex;
		flex-direction: column;
		gap: var(--space-5);
		align-items: center;
		text-align: center;
	}

	.mobile-link {
		font-family: var(--font-headline);
		font-size: var(--text-base);
		font-weight: 500;
		color: var(--color-lime);
		text-decoration: none;
		letter-spacing: 0.1em;
	}

	@media (max-width: 900px) {
		.desktop-nav {
			display: none;
		}
		.mobile-toggle {
			display: flex;
			align-items: center;
			justify-content: center;
		}
	}
</style>
