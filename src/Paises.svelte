<script>
	import { onMount } from 'svelte';

    let value = "";

    var url = `https://disease.sh/v3/covid-19/countries/${value}`;
    var urlTodosLosPaises = `https://disease.sh/v3/covid-19/countries`;

    //VARIABLES WORLDOMETER

    let nombrePaisWorldometerLC;
    let nombrePaisWorldometer;
    let casosPaisWorldometer;
    let muertesPaisWorldometer;
    let muertesPaisHoyWorldometer;
    let casosPaisHoyWorldometer;
    let casosActivosPaisWorldometer;
    let muertesPorMillonWorldometer;
    let poblacionWorldometer;
    let continenteWorldometer;

    let estado = "oculto";

    // Obtenemos lista de paises
    let listaPaises = [];
    onMount( () => {
        fetch(urlTodosLosPaises).
          then ( res => res.json()).
          then ( data => { 
              listaPaises = data.map( x => x.country);
              value = listaPaises[0];
              onChange();             
          });
    });

    let nombrePais;
    let casos;

    let labelsCasos = [];
    let dataCasos = [];

    let myChart = new Chart();

    function onChange(){
        fetch(`https://disease.sh/v3/covid-19/countries/${value}`)
            .then((response) => response.json())
            .then((pais) => {
                nombrePaisWorldometerLC = pais.country.toLowerCase;
                if (value.toLowerCase == nombrePaisWorldometerLC) {
                    nombrePaisWorldometer = pais.country;
                    casosPaisWorldometer = pais.cases;
                    muertesPaisWorldometer = pais.deaths;
                    muertesPaisHoyWorldometer = pais.todayDeaths;
                    casosPaisHoyWorldometer = pais.todayCases;
                    casosActivosPaisWorldometer = pais.active;
                    muertesPorMillonWorldometer = pais.deathsPerOneMillion;
                    poblacionWorldometer = pais.population;
                    continenteWorldometer = pais.continent;
                    estado = "visible";
                }
            });
        
    
 
        /* GRAFICA    */

        fetch(`https://disease.sh/v3/covid-19/historical/${value}?lastdays=30`)
            .then((response) => response.json())
            .then((casosPais) => {
                console.log("PAIS: " + casosPais.country);
                casos = casosPais.timeline.cases;
                nombrePais = casosPais.country.toLowerCase;
                if (value.toLowerCase == nombrePais) {
                    //console.log(casosPais.timeline.cases);

                    labelsCasos = Object.keys(casosPais.timeline.cases);
                    dataCasos = Object.values(casosPais.timeline.cases);
                    labelsCasos = labelsCasos.map( x => x.split("/"))
                                             .map( x => x[1]+"/"+x[0]+"/"+x[2]);
               
                    // INICIO GRAFICA 

                    let ctx = document.getElementById("grafica").getContext('2d');
                    myChart.destroy();
                    myChart = new Chart(ctx, {
                        type: "line",
                        data: {
                            labels: labelsCasos,
                            datasets: [
                                {
                                    label: "Casos",
                                    borderColor: "#F10808",
                                    hoverBorderColor: "green",
                                    pointColor: "rgba(210, 214, 222, 1)",
                                    pointStrokeColor: "#c1c7d1",
                                    pointHighlightFill: "#fff",
                                    pointHighlightStroke: "rgba(220,220,220,1)",
                                    data: dataCasos
                                },
                            ],
                        },
                    });

                }

            });

    }



</script>


<select bind:value on:change={onChange}>
	{#each listaPaises as pais}
		<option value={pais}>{pais}</option> 
	{/each}
</select>


    <!-- Div principal del muestreo de datos de la pagina -->
    <div class={estado} id="datosPais">
        <h6 class="centrado">Según Woldometer</h6>
        <h1>{nombrePaisWorldometer} ({continenteWorldometer})</h1>
        <h4 class="centrado">{poblacionWorldometer} habitantes</h4>
        <h3>
            Casos totales: <span class="resaltarDato"
                >{casosPaisWorldometer}</span
            >
            - Muertos:
            <span class="resaltarDato">{muertesPaisWorldometer}</span>
        </h3>

        <h3>
            Casos positivos hoy: <span class="resaltarDato"
                >{casosPaisHoyWorldometer}</span
            >
            <br />
            Muertes hoy:
            <span class="resaltarDato">{muertesPaisHoyWorldometer}</span>
        </h3>
        <h3>
            Casos positivos actualmente <span class="resaltarDato"
                >{casosActivosPaisWorldometer}</span
            >
        </h3>
        <h3>
            Casos positivos totales: <span class="resaltarDato"
                >{casosPaisWorldometer}</span
            >
            <br />
            Muertes totales:
            <span class="resaltarDato">{muertesPaisWorldometer}</span>
        </h3>

        <h3>
            Incidencia total de <span class="resaltarDato"
                >{muertesPorMillonWorldometer}</span
            > por millon de habitantes
        </h3>
        

            <h3> GRAFICA DE CASOS</h3>
            <canvas id="grafica" width="400" height="400" />
  
        <!-- <canvas id="grafica" width="400" height="400" /> --> 
    </div>


<style>
    .oculto {
        display: none;
    }
    .visible {
        display: block;
    }
    .resaltarDato {
        color: red;
    }

    #datosPais {
        margin-left: auto;
        margin-right: auto;
        width: 50%;
        text-align: left;
        background-color: #a9cce3;
        /* border-radius: 10%; */
        border-radius: 1em;
        padding: 1%;
    }
    #datosPais h1 {
        color: black;
        text-transform: uppercase;
        font-style: italic;
        font-family: "Franklin Gothic Medium", "Arial Narrow", Arial, sans-serif;
        text-align: center;
        font-size: 50px;
        line-height: 5px;
    }
    .centrado {
        text-align: center;
    }

    @media (max-width: 1024px) {
        .oculto {
            display: none;
        }
        .visible {
            display: block;
        }
        .resaltarDato {
            /* color: red; */
            color: #871a03;
        }

        #datosPais {
            margin-left: auto;
            margin-right: auto;
            width: 100%;
            text-align: left;
            background-color: #a9cce3;
            /* border-radius: 10%; */
            border-radius: 1em;
            padding: 1%;
            font-size: 10px;
        }
        #datosPais h1 {
            color: black;
            text-transform: uppercase;
            font-style: italic;
            font-family: "Franklin Gothic Medium", "Arial Narrow", Arial,
                sans-serif;
            text-align: center;
            font-size: 25px;
            line-height: 5px;
        }
        .centrado {
            text-align: center;
        }
    }

    @media (max-width: 765px) {
        .oculto {
            display: none;
        }
        .visible {
            display: block;
        }
        .resaltarDato {
            /* color: red; */
            color: #871a03;
        }

        #datosPais {
            margin-left: auto;
            margin-right: auto;
            width: 100%;
            text-align: left;
            background-color: #a9cce3;
            /* border-radius: 10%; */
            border-radius: 1em;
            padding: 1%;
        }
        #datosPais {
            font-size: 8px;
        }
        #datosPais h1 {
            color: black;
            text-transform: uppercase;
            font-style: italic;
            font-family: "Franklin Gothic Medium", "Arial Narrow", Arial,
                sans-serif;
            text-align: center;
            font-size: 15px;
            line-height: 5px;
        }
        .centrado {
            text-align: center;
        }
    }
</style>