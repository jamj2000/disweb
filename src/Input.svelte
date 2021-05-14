<script>
    let value = "";
    const handleInput = (event) => (value = event.target.value);
    
    
    
    var url = `https://disease.sh/v3/covid-19/countries/${value}`;
    let nombreOficial;
    let casosPais;
    let muertesPais;
    let muertesPaisHoy;
    let casosPaisHoy;
    let casosActivosPais;
    let muertesPorMillon;
    let poblacion;
    let continente;

    $: estado = "oculto";
    $: if (value.length > 3) {
        fetch(`https://disease.sh/v3/covid-19/countries/${value}`)
            .then((response) => response.json())
            .then((pais) => {
                console.log(pais);
                console.log(pais.country);
                console.log(value);
                
                
                if (value.toLowerCase == pais.country.toLowerCase) {
                    nombreOficial = pais.country;
                    casosPais = pais.cases;
                    muertesPais = pais.deaths;
                    muertesPaisHoy = pais.todayDeaths;
                    casosPaisHoy = pais.todayCases;
                    casosActivosPais = pais.active;
                    muertesPorMillon = pais.deathsPerOneMillion;
                    poblacion = pais.population;
                    continente = pais.continent;
                    estado = "visible";
                    
                }
                
                
            });
            
    }


     var urlTodosLosPaises = `https://disease.sh/v3/covid-19/countries`;
   /* fetch(urlTodosLosPaises)
            .then((response) => response.json())
            .then((paises) => {
                //console.log(paises.length);
                var element = document.getElementById("listado");
                for(var i = 0; i <paises.length; i++){
                    //console.log(paises[i].country)
                    element.innerHTML += paises[i].country + " - " 
                }

                
                
            }); */



            fetch(urlTodosLosPaises)
            .then((response) => response.json())
            .then((paises) => {
                console.log(paises.length);
                var element = document.getElementById("listadoSelect");

                for(var i = 0; i <paises.length; i++){
                    //console.log(paises[i].country)
                    var paisSeleccionado = paises[i].country;
                    console.log("Pais seleccionado" + paisSeleccionado)
                    element.innerHTML += `<option value="${i}"> ${paisSeleccionado}</option>`;
                    console.log("Pais seleccionado DESPUES" + paisSeleccionado)
                }

                fetch(`https://disease.sh/v3/covid-19/countries/${paisSeleccionado}`)
            .then((response) => response.json())
            .then((pais) => {
                console.log(pais);
                console.log(pais.country);
                console.log(value);
                
                
                if (value.toLowerCase == pais.country.toLowerCase) {
                    nombreOficial = pais.country;
                    casosPais = pais.cases;
                    muertesPais = pais.deaths;
                    muertesPaisHoy = pais.todayDeaths;
                    casosPaisHoy = pais.todayCases;
                    casosActivosPais = pais.active;
                    muertesPorMillon = pais.deathsPerOneMillion;
                    poblacion = pais.population;
                    continente = pais.continent;
                    estado = "visible";
                    
                }
                
                
            });
                
            });

            
</script>



<main>
    <input
        type="text"
        {value}
        on:input={handleInput}
        placeholder="Escribir país en Inglés"
        size="30"
    />
    <select name="" id="">
        <option value="" on:select={handleSelect} ></option>
    </select>



    <h2 class={estado}>
        <h1>{nombreOficial}</h1>
        <h3>con casos totales: {casosPais} y {muertesPais} muertos</h3>
       
        <h3>
            Casos positivos: {casosPaisHoy} <br> Muertes:  {muertesPaisHoy}
            
        </h3>

        <h2>Casos positivos actuales {casosActivosPais}</h2>
        <h2>Incidencia total de {muertesPorMillon} por millon de habitantes</h2>

        <h2>
            {nombreOficial} pertenece a {continente} y tiene {poblacion} habitantes
        </h2>
    </h2>

    <!-- <h2>
        <h1>{nombreOficial}</h1>
        <h3>con casos totales: {casosPais} y {muertesPais} muertos</h3>
       
        <h3>
            Casos positivos: {casosPaisHoy} <br> Muertes:  {muertesPaisHoy}
            
        </h3>

        <h2>Casos positivos actuales {casosActivosPais}</h2>
        <h2>Incidencia total de {muertesPorMillon} por millon de habitantes</h2>

        <h2>
            {nombreOficial} pertenece a {continente} y tiene {poblacion} habitantes
        </h2>
    </h2> -->
    <h2>Lista de paises para buscar</h2>
    <p id="listado"> </p>

    <select name="" id="listadoSelect">
        
    </select>
</main>

<style>
    .oculto {
        display: none;
    }
    .visible {
        display: block;
    }
</style>
