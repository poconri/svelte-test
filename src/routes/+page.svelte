<script>
	import Counter from './Counter.svelte';
	import welcome from '$lib/images/svelte-welcome.webp';
	import welcome_fallback from '$lib/images/svelte-welcome.png';
	import HeroesList from './HeroesList.svelte';
</script>

<svelte:head>
	<title>Heroes</title>
	<meta name="description" content="Heroes App" />
</svelte:head>

<section>
	<!-- <Counter /> -->
	<HeroesList />
</section>

<style>
	
</style>
