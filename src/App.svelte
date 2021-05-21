<script>
	import InputBuscadorDePais from "./Input.svelte";

	export let name;

	import { Router } from "svelte-routing";
	import Nav from "./Nav.svelte";
	import Contenido from "./Contenido.svelte";

	/* let globalDeaths;

	fetch("https://disease.sh/v3/covid-19/all")
		.then((response) => response.json())
		.then((global) => {
			globalDeaths = global.deaths;
		});

	let nombrePais;
	nombrePais = "spain";

	var url = "https://disease.sh/v3/covid-19/countries/" + nombrePais;

	let nombreOficial;
	let casosPais;
	let muertesPais;
	let muertesPaisHoy;
	let casosPaisHoy;
	let casosActivosPais;
	let muertesPorMillon;
	let poblacion;
	let continente;

	fetch(url)
		.then((response) => response.json())
		.then((pais) => {
			nombreOficial = pais.country;
			casosPais = pais.cases;
			muertesPais = pais.deaths;
			muertesPaisHoy = pais.todayDeaths;
			casosPaisHoy = pais.todayCases;
			casosActivosPais = pais.active;
			muertesPorMillon = pais.deathsPerOneMillion;
			poblacion = pais.population;
			continente = pais.continent;
		});


	var urlTodosLosPaises = `https://disease.sh/v3/covid-19/countries`;
	fetch(urlTodosLosPaises)
		.then((response) => response.json())
		.then((paises) => {
			//console.log(paises.length);
			var element = document.getElementById("listado");
			for (var i = 0; i < paises.length; i++) {
				//console.log(paises[i].country)
				element.innerHTML += paises[i].country + " - ";
			}
		}); */
</script>

<main>
	<Router>
		<Nav />
		<Contenido />
	</Router>
	<!-- <h3>Busqueda de países:</h3>
	<p>
		Escoge cualquier pais de la lista anterior para ver sus datos
		relacionados con el covid-19
	</p>
	<InputBuscadorDePais />
	<footer>
	<h2>Lista de paises para buscar</h2>
	<p id="listado" />	
	</footer> -->
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
	#listado {
		font-weight: bold;
		width: 100%;
	}

	@media (max-width: 1024px) {
		#listado {
			font-size: 10px;
		}
	}
	@media (max-width: 765px) {
		#listado {
			font-size: 5px;
		}
	}
</style>
