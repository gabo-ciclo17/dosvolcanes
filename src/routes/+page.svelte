<script lang="ts">
	import Navbar from '$cliente/Navbar.svelte';
	import HeroSection from '$cliente/HeroSection.svelte';
	import FeaturesSection from '$cliente/FeaturesSection.svelte';
	import MasterplanSection from '$cliente/MasterplanSection.svelte';
	import LocationSection from '$cliente/LocationSection.svelte';
	import GallerySection from '$cliente/GallerySection.svelte';
	import ContactFooterSection from '$cliente/ContactFooterSection.svelte';
</script>

<svelte:head>
	<title>Dos Volcanes Rupanco — Proyecto Exclusivo en X Región, Chile</title>
	<meta
		name="description"
		content="Descubre Dos Volcanes Rupanco: 28 lotes exclusivos de 5.000 m² con orilla de lago, derechos de agua inscritos, masterplan 360º y naturaleza virgen en la X Región de Chile."
	/>
	<meta property="og:title" content="Dos Volcanes Rupanco — Proyecto Exclusivo" />
	<meta
		property="og:description"
		content="Parcelas exclusivas en Lago Rupanco con bosque nativo, orilla de lago y conectividad privilegiada."
	/>
	<meta property="og:type" content="website" />
</svelte:head>

<main class="page-layout">
	<Navbar />
	<HeroSection />
	<FeaturesSection />
	<MasterplanSection />
	<LocationSection />
	<GallerySection />
	<ContactFooterSection />
</main>

<style>
	.page-layout {
		width: 100%;
		min-height: 100vh;
		background: var(--color-plum);
		color: var(--color-ecru);
		font-family: var(--font-body);
		overflow-x: hidden;
		display: flex;
		flex-direction: column;
	}
</style>
