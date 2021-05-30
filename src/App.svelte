<script>

	import { Router } from "svelte-routing";
	import Nav from "./Nav.svelte";
	import Contenido from "./Contenido.svelte";

	
</script>

<main>
	<Router>
		<Nav />
		<Contenido />
	</Router>
	
</main>

<style>
	:global(body) {
		background-color: #a58faa;
		margin: 0;
		padding: 0;
		font-display: swap; /* Para mejorar rendimiento en carga inicial */
	}
	:global(a:hover) {
		text-decoration: none;
		cursor: pointer;
	}
	main {
		text-align: center;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}
	h2 {
		color: gray;
		font-size: medium;
	}
	h3 {
		color: blue;
		font-size: xx-large;
	}
	
</style>
