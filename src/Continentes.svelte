<script>
    import { onMount } from "svelte";

    let value = "";

    var urlTodosLosContinentes = `https://disease.sh/v3/covid-19/continents`;

    //VARIABLES WORLDOMETER Continentes

    //DATOS DEL PAIS
    let nombreContinenteWorldometerLC;
    let nombreContinenteWorldometer;
    let latitudContinenteWorldometer;
    let longitudContinenteWorldometer;

    //GENERAL / TOTAL
    let casosContinenteWorldometer;
    let muertesContinenteWorldometer;
    let recuperadosContinenteWorldometer;
    let testRealizadosWorldometer;
    let poblacionWorldometer;
    //HOY

    let muertesContinenteHoyWorldometer;
    let casosContinenteHoyWorldometer;
    let recuperadosContinenteHoyWorldometer;
    let casosActivosContinenteWorldometer;
    let casosCriticosWorldometer;

    //TASAS
    let casosPorMillonWorldometer;
    let muertesPorMillonWorldometer;
    let casosActivosPorMillonWorldometer;
    let testPorMillonWorldometer;
    let recuperadosPorMillonWorldometer;
    let criticosPorMillonWorldometer;

    // Obtenemos lista de Continentes
    let listaContinentes = [];
    onMount(() => {
        fetch(urlTodosLosContinentes)
            .then((res) => res.json())
            .then((data) => {
                listaContinentes = data.map((x) => x.continent);
                value = listaContinentes[0];
                onChange();
            });
    });

    function onChange() {
        fetch(`https://disease.sh/v3/covid-19/continents/${value}`)
            .then((response) => response.json())
            .then((continente) => {
                nombreContinenteWorldometerLC =
                    continente.continent.toLowerCase;
                if (value.toLowerCase == nombreContinenteWorldometerLC) {
                    //DATOS DEL PAIS
                    nombreContinenteWorldometer = continente.continent;
                    latitudContinenteWorldometer = continente.continentInfo.lat;
                    longitudContinenteWorldometer =
                        continente.continentInfo.long;

                    //HOY

                    muertesContinenteHoyWorldometer = continente.todayDeaths;
                    casosContinenteHoyWorldometer = continente.todayCases;
                    recuperadosContinenteHoyWorldometer =
                        continente.todayRecovered;
                    casosActivosContinenteWorldometer = continente.active;
                    casosCriticosWorldometer = continente.critical;

                    //GENERAL / TOTAL
                    casosContinenteWorldometer = continente.cases;
                    muertesContinenteWorldometer = continente.deaths;
                    recuperadosContinenteWorldometer = continente.recovered;
                    testRealizadosWorldometer = continente.tests;
                    poblacionWorldometer = continente.population;

                    //TASAS
                    casosPorMillonWorldometer = continente.casesPerOneMillion;
                    muertesPorMillonWorldometer =
                        continente.deathsPerOneMillion;
                    casosActivosPorMillonWorldometer =
                        continente.activePerOneMillion;
                    testPorMillonWorldometer = continente.testsPerOneMillion;
                    recuperadosPorMillonWorldometer =
                        continente.recoveredPerOneMillion;
                    criticosPorMillonWorldometer =
                        continente.criticalPerOneMillion;
                }
            });
    }
</script>

<select bind:value on:change={onChange} class="selectContinente">
    {#each listaContinentes as continente}
        <option value={continente}>{continente}</option>
    {/each}
</select>

<!-- Div principal del muestreo de datos de la pagina -->
<div id="datosContinente">
    <h6 class="centrado">Según Woldometer</h6>

    <div class="divBandera">
        <span class="nombrePais">
            {nombreContinenteWorldometer}
        </span>
    </div>
    <h5 class="centrado">
        Lat: {latitudContinenteWorldometer} - Long: {longitudContinenteWorldometer}
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
                        {casosContinenteWorldometer}
                    </span>
                </p>
                <p>
                    Tests: <span class="cifra">
                        {testRealizadosWorldometer}</span
                    >
                </p>
                <p>
                    Muertes: <span class="cifra">
                        {muertesContinenteWorldometer}</span
                    >
                </p>
                <p>
                    Recuperaciones: <span class="cifra"
                        >{recuperadosContinenteWorldometer}
                    </span>
                </p>
            </div>
        </div>
        <div class="hoy divDatos">
            <h3 class="subtitulo">DATOS HOY</h3>
            <div class="datos">
                <p>
                    Casos: <span class="cifra">
                        {casosContinenteHoyWorldometer}
                    </span>
                </p>
                <p>
                    Activos: <span class="cifra">
                        {casosActivosContinenteWorldometer}</span
                    >
                </p>
                <p>
                    Criticos: <span class="cifra">
                        {casosCriticosWorldometer}</span
                    >
                </p>
                <p>
                    Muertes: <span class="cifra">
                        {muertesContinenteHoyWorldometer}</span
                    >
                </p>
                <p>
                    Recuperaciones: <span class="cifra"
                        >{recuperadosContinenteHoyWorldometer}
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
    .selectContinente {
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
    .divBandera {
        border-radius: 1em;
        box-shadow: 0px 1px 10px grey;
        text-align: center;
        background-position: center;
        background-size: auto;
        background-repeat: no-repeat;
        height: 180px;
    }
    .nombrePais {
        text-transform: uppercase;
        font-style: italic;
        height: 100px;
        font-size: 50px;
        padding: 10px;
        background-color: rgba(245, 245, 245, 0.604);
        border-radius: 1em;
        position: relative;
        top: 60px;
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
        box-shadow: 0px 1px 10px #bc1333;
    }
    .divDatos:hover .subtitulo {
        color: #bc1333;
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

    #datosContinente {
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
    #datosContinente h1 {
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
        .divDatos {
            height: 200px;
        }
        #datosContinente {
            width: 95%;
            font-size: 10px;
        }
        #datosContinente h1 {
            font-size: 35px;
        }
        .centrado {
            text-align: center;
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
        #datosContinente {
            margin-left: auto;
            margin-right: auto;
            width: 95%;
            text-align: left;
            background-color: rgba(245, 245, 245, 0.604);
            border-radius: 1em;
            padding: 1%;
            padding-bottom: 5%;
        }
        #datosContinente {
            font-size: 8px;
        }
        #datosContinente h1 {
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
        .divBandera {
            border-radius: 1em;
            box-shadow: 0px 1px 10px grey;
            text-align: center;
            background-position: center;
            background-size: auto;
            background-repeat: no-repeat;
            height: 150px;
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
            top: 60px;
        }
    }
</style>
