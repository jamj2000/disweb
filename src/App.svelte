<script>
	export let name;


	let globalDeaths;

    fetch('https://disease.sh/v3/covid-19/all')
        .then((response) => response.json())
        .then((global) => {
            globalDeaths = global.deaths;
        });

	let nombrePais;
	nombrePais = 'spain';

	var url = 'https://disease.sh/v3/covid-19/countries/'+ nombrePais;

	
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

		
import InputBuscadorDePais from "./Input.svelte";


</script>

<main>
	<!-- <h1>Hello {name}!</h1>
	<p>Visit the <a href="https://svelte.dev/tutorial">Svelte tutorial</a> to learn how to build Svelte apps.</p> -->

	<!-- <h1>Muertos globales por covid: {globalDeaths}</h1> -->
	<!-- <h2>URL: {url}</h2> -->
	<!-- <h2> Pais: {nombreOficial} con casos totales: {casosPais} y {muertesPais} muertos <br> 
		hoy hay {casosPaisHoy} casos positivos y han muerto {muertesPaisHoy} personas <br>
	casos positivos actuales {casosActivosPais} y una incidencia total de {muertesPorMillon} por millon de habitantes <br>
pertenece a {continente} y tiene {poblacion} habitantes</h2> -->

<h3> Busqueda de países: </h3>
<InputBuscadorDePais />
	

</main>








<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}
	h2{
		color: gray;
		font-size: medium;
	}
	h3{
		color: blue;
		font-size: xx-large;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>