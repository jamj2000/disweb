<script>
    import { onMount } from "svelte";

    let value = "";

    var url = `https://disease.sh/v3/covid-19/countries/${value}`;
    var urlTodosLosPaises = `https://disease.sh/v3/covid-19/countries`;

    //VARIABLES WORLDOMETER

    //VARIABLES WORLDOMETER Paises

    //DATOS DEL PAIS
    let banderaPais;
    let nombrePaisWorldometerLC;
    let nombrePaisWorldometer;
    let latitudPaisWorldometer;
    let longitudPaisWorldometer;
    let paisContinente;

    //GENERAL / TOTAL
    let casosPaisWorldometer;
    let muertesPaisWorldometer;
    let recuperadosPaisWorldometer;
    let testRealizadosWorldometer;
    let poblacionWorldometer;
    //HOY

    let muertesPaisHoyWorldometer;
    let casosPaisHoyWorldometer;
    let recuperadosPaisHoyWorldometer;
    let casosActivosPaisWorldometer;
    let casosCriticosWorldometer;

    //TASAS
    let casosPorMillonWorldometer;
    let muertesPorMillonWorldometer;
    let casosActivosPorMillonWorldometer;
    let testPorMillonWorldometer;
    let recuperadosPorMillonWorldometer;
    let criticosPorMillonWorldometer;

    let estado = "oculto";

    // Obtenemos lista de paises
    let listaPaises = [];
    onMount(() => {
        fetch(urlTodosLosPaises)
            .then((res) => res.json())
            .then((data) => {
                listaPaises = data.map((x) => x.country);
                value = listaPaises[0];
                onChange();
            });
    });

    let nombrePais;
    let casos;

    let labelsCasos = [];
    let dataCasos = [];

    let myChart = new Chart();

    function onChange() {
        fetch(`https://disease.sh/v3/covid-19/countries/${value}`)
            .then((response) => response.json())
            .then((pais) => {
                nombrePaisWorldometerLC = pais.country.toLowerCase;
                if (value.toLowerCase == nombrePaisWorldometerLC) {
                    //DATOS DEL PAIS
                    banderaPais = pais.countryInfo.flag;
                    nombrePaisWorldometer = pais.country;
                    latitudPaisWorldometer = pais.countryInfo.lat;
                    longitudPaisWorldometer = pais.countryInfo.long;
                    paisContinente = pais.continent;

                    //HOY

                    muertesPaisHoyWorldometer = pais.todayDeaths;
                    casosPaisHoyWorldometer = pais.todayCases;
                    recuperadosPaisHoyWorldometer = pais.todayRecovered;
                    casosActivosPaisWorldometer = pais.active;
                    casosCriticosWorldometer = pais.critical;

                    //GENERAL / TOTAL
                    casosPaisWorldometer = pais.cases;
                    muertesPaisWorldometer = pais.deaths;
                    recuperadosPaisWorldometer = pais.recovered;
                    testRealizadosWorldometer = pais.tests;
                    poblacionWorldometer = pais.population;

                    //TASAS
                    casosPorMillonWorldometer = pais.casesPerOneMillion;
                    muertesPorMillonWorldometer = pais.deathsPerOneMillion;
                    casosActivosPorMillonWorldometer = pais.activePerOneMillion;
                    testPorMillonWorldometer = pais.testsPerOneMillion;
                    recuperadosPorMillonWorldometer =
                        pais.recoveredPerOneMillion;
                    criticosPorMillonWorldometer = pais.criticalPerOneMillion;
                }
            });

        /* GRAFICA    */

        /* fetch(`https://disease.sh/v3/covid-19/historical/${value}?lastdays=30`)
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

            }); */
    }
</script>

<select bind:value on:change={onChange} class="selectPais">
    {#each listaPaises as pais}
        <option value={pais}>{pais}</option>
    {/each}
</select>

<!-- Div principal del muestreo de datos de la pagina -->

<div id="datosPais">
    <h6 class="centrado">Según Woldometer</h6>
    <div class="divBandera" style="background-image: url({banderaPais});">
        <span class="nombrePais">
            {nombrePaisWorldometer}
        </span>
    </div>

    <h5 class="centrado">
        Lat: {latitudPaisWorldometer} - Long: {longitudPaisWorldometer}
    </h5>

    <div class="contenedor">
        <div class="general divDatos">
            <h3 class="subtitulo">DATOS TOTALES</h3>
            <div class="datos">
                <p>
                    Poblacion: <span class="cifra">
                        {poblacionWorldometer}</span
                    >
                </p>
                <p>
                    Casos: <span class="cifra">
                        {casosPaisWorldometer}
                    </span>
                </p>
                <p>
                    Tests: <span class="cifra">
                        {testRealizadosWorldometer}</span
                    >
                </p>
                <p>
                    Muertes: <span class="cifra">
                        {muertesPaisWorldometer}</span
                    >
                </p>
                <p>
                    Recuperaciones: <span class="cifra"
                        >{recuperadosPaisWorldometer}
                    </span>
                </p>
            </div>
        </div>
        <div class="hoy divDatos">
            <h3 class="subtitulo">DATOS HOY</h3>
            <div class="datos">
                <p>
                    Casos: <span class="cifra">
                        {casosPaisHoyWorldometer}
                    </span>
                </p>
                <p>
                    Activos: <span class="cifra">
                        {casosActivosPaisWorldometer}</span
                    >
                </p>
                <p>
                    Criticos: <span class="cifra">
                        {casosCriticosWorldometer}</span
                    >
                </p>
                <p>
                    Muertes: <span class="cifra">
                        {muertesPaisHoyWorldometer}</span
                    >
                </p>
                <p>
                    Recuperaciones: <span class="cifra"
                        >{recuperadosPaisHoyWorldometer}
                    </span>
                </p>
            </div>
        </div>
        <div class="tasas divDatos">
            <h3 class="subtitulo">TASAS (x millon/habs)</h3>
            <div class="datos">
                <p>
                    Tests: <span class="cifra">
                        {testPorMillonWorldometer}
                    </span>
                </p>
                <p>
                    Casos : <span class="cifra">
                        {casosPorMillonWorldometer}
                    </span>
                </p>
                <p>
                    Activos: <span class="cifra">
                        {casosActivosPorMillonWorldometer}</span
                    >
                </p>
                <p>
                    Criticos: <span class="cifra">
                        {casosActivosPorMillonWorldometer}</span
                    >
                </p>
                <p>
                    Muertes: <span class="cifra">
                        {muertesPorMillonWorldometer}</span
                    >
                </p>
                <p>
                    Recuperaciones: <span class="cifra"
                        >{recuperadosPorMillonWorldometer}
                    </span>
                </p>
            </div>
        </div>
    </div>
</div>

<style>
    * {
        font-family: "Franklin Gothic Medium", "Arial Narrow", Arial, sans-serif;
    }
    .selectPais {
        margin-top: 30px;
        width: 50%;
    }
    .contenedor {
        display: flex;
        flex-direction: row;
        flex-wrap: wrap;
        justify-content: space-evenly;
        align-items: flex-start;
    }
    .nombrePais {
        text-transform: uppercase;

        font-style: italic;
        height: 100px;
        font-size: 30px;
        padding: 10px;
        background-color: rgba(245, 245, 245, 0.604);
        border-radius: 1em;
        position: relative;
        top: 70px;
    }

    .divDatos {
        text-align: center;
        height: 300px;
        width: 30%;
        border-radius: 1em;
        background-color: rgba(0, 0, 0, 0.761);
        box-shadow: 0px 1px 10px #a6d6d6;
    }

    .divDatos:hover {
        transition: transform 0.2s linear;
        transform: scale(1.2);
        box-shadow: 0px 1px 10px #BC1333;
    }
    .divDatos:hover .subtitulo {
        color: #BC1333;
    }
    .subtitulo {
        padding-bottom: 5px;
        border-bottom: 1px solid rgba(255, 255, 255, 0.72);
        color: #a6d6d6;
    }
    .datos p {
        color: whitesmoke;
        font-weight: bold;
    }
    .cifra {
        font-weight: normal;
    }

    #datosPais {
        margin-left: auto;
        margin-right: auto;
        margin-top: 20px;
        width: 90%;
        text-align: left;
        background-color: rgba(245, 245, 245, 0.604);
        border-radius: 1em;
        padding: 1%;
        padding-bottom: 5%;
    }
    .divBandera {
        border-radius: 1em;
        box-shadow: 0px 1px 10px grey;
        text-align: center;
        background-position: center;
        background-size: auto;
        background-repeat: no-repeat;
        height: 180px;
    }

    .centrado {
        text-align: center;
    }

    @media (max-width: 1024px) {
        .divDatos {
            height: 200px;
        }
        #datosPais {
            margin-left: auto;
            margin-right: auto;
            width: 95%;
            text-align: left;
            background-color: rgba(245, 245, 245, 0.604);
            border-radius: 1em;
            padding: 1%;
            padding-bottom: 5%;
            font-size: 10px;
        }
        #datosPais h1 {
            color: black;
            text-transform: uppercase;
            font-style: italic;
            font-family: "Franklin Gothic Medium", "Arial Narrow", Arial,
                sans-serif;
            text-align: center;
            font-size: 35px;
            line-height: 5px;
        }
        .centrado {
            text-align: center;
        }
        .nombrePais {
            text-transform: uppercase;
            font-style: italic;
            height: 100px;
            font-size: 20px;
            padding: 10px;
            background-color: rgba(245, 245, 245, 0.604);
            border-radius: 1em;
            position: relative;
            top: 50px;
        }
        .divBandera {
            text-align: center;
            background-position: center;
            background-size: auto;
            background-repeat: no-repeat;
            height: 130px;
        }
    }

    @media (max-width: 765px) {
        .divDatos {
            margin-top: 20px;
            margin-bottom: 10px;
            height: 250px;
            width: 80%;
        }
        .contenedor {
            display: flex;
            flex-direction: column;
            flex-wrap: wrap;
            justify-content: space-evenly;
            align-items: center;
        }
        .subtitulo {
            font-size: 20px;
        }
        .datos p {
            color: whitesmoke;
            font-weight: bold;
            font-size: 12px;
        }
        .cifra {
            font-weight: normal;
        }
        #datosPais {
            margin-left: auto;
            margin-right: auto;
            width: 95%;
            text-align: left;
            background-color: rgba(245, 245, 245, 0.604);
            border-radius: 1em;
            padding: 1%;
            padding-bottom: 5%;
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
            font-size: 30px;
            line-height: 5px;
        }
        .centrado {
            text-align: center;
        }

        .nombrePais {
            text-transform: uppercase;
            font-style: italic;
            height: 100px;
            font-size: 15px;
            padding: 10px;
            background-color: rgba(245, 245, 245, 0.604);
            border-radius: 1em;
            position: relative;
            top: 45px;
        }
        .divBandera {
            text-align: center;
            background-position: center;
            background-size: auto;
            background-repeat: no-repeat;
            height: 110px;
        }
    }
</style>
