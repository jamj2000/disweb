<script>
    let value = "";
    //const handleInput = (event) => (value = event.target.value);
    const handleSelect = (event) => (value = event.target.value);

    var url = `https://disease.sh/v3/covid-19/countries/${value}`;
    var urlTodosLosPaises = `https://disease.sh/v3/covid-19/countries`;

    let nombrePaisWorldometer;
    let casosPaisWorldometer;
    let muertesPaisWorldometer;
    let muertesPaisHoyWorldometer;
    let casosPaisHoyWorldometer;
    let casosActivosPaisWorldometer;
    let muertesPorMillonWorldometer;
    let poblacionWorldometer;
    let continenteWorldometer;

    function mostrarPais(){

        
    }

    fetch(`https://disease.sh/v3/covid-19/countries`)
        .then((response) => response.json())
        .then((paises) => {
            
            console.log(paises.length);
            var elemento = document.getElementById("selectPais");
            for(var i = 0; i<paises.length; i++){
                elemento.innerHTML += `<option value="${i}"> ${paises[i].country} </option>`;

                
            }

        });



    fetch(`https://disease.sh/v3/covid-19/countries/${value}`)
        .then((response) => response.json())
        .then((pais) => {});
    /*







<option value=""> </option>



    
    */

    //VARIABLES WORLDOMETER

    /*  let nombrePaisWorldometer;
    let casosPaisWorldometer;
    let muertesPaisWorldometer;
    let muertesPaisHoyWorldometer;
    let casosPaisHoyWorldometer;
    let casosActivosPaisWorldometer;
    let muertesPorMillonWorldometer;
    let poblacionWorldometer;
    let continenteWorldometer;

    $: estado = "oculto";
    $: if (value.length > 3) {
        fetch(`https://disease.sh/v3/covid-19/countries/${value}`)
            .then((response) => response.json())
            .then((pais) => {
                var nombrePaisWorldometerLC = pais.country.toLowerCase;
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
    } */

    /*
GRAFICA
    */

   /*  let nombrePais;
    let casos;

    $: labelsCasos = [];
    $: dataCasos = [];
    var myChart = new Chart(); */

    /* 
    $: myChart = new Chart(ctx, {
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
                                    data: dataCasos,
                                },
                            ],
                        },
                    });
 */
    /* $: if (value.length > 3) {
        console.log("Dentro del IF para grafica");
        fetch(`https://disease.sh/v3/covid-19/historical/${value}?lastdays=15`)
            .then((response) => response.json())
            .then((casosPais) => {
                console.log("PAIS: " + casosPais.country);
                casos = casosPais.timeline.cases;
                nombrePais = casosPais.country.toLowerCase;
                if (value.toLowerCase == nombrePais) {
                    //console.log(casosPais.timeline.cases);

                    labelsCasos = Object.keys(casosPais.timeline.cases);
                    dataCasos = Object.values(casosPais.timeline.cases);

                    // INICIO GRAFICA 

                    let ctx = document.getElementById("grafica").getContext('2d');
                    let myChart = new Chart(ctx, {
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
                                    data: dataCasos,
                                },
                            ],
                        },
                    });

                    //FIN GRAFICA 
                }
                console.log("Fuera");
            });
    } */

    /* $: if (value.length < 3) {
        myChart.destroy();
        console.log("destruida");
    } */
</script>

<main>
    <!-- <input
        type="text"
        {value}
        on:input={handleInput}
        placeholder="Escribir país en Inglés"
        size="30"
    /> -->

    <select name="" id="selectPais" onchange="mostrarPais()">
        
    </select>

    <!-- Div principal del muestreo de datos de la pagina -->
    <!-- class={estado} -->
    <div  id="datosPais">
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

        <!-- <details>
            <summary> GRAFICA DE CASOS</summary>
            <canvas id="grafica" width="400" height="400" />
        </details> -->
        <!-- <canvas id="grafica" width="400" height="400" /> -->
    </div>
</main>

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
        border-radius: 10%;
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
            color: red;
        }

        #datosPais {
            margin-left: auto;
            margin-right: auto;
            width: 100%;
            text-align: left;
            background-color: #a9cce3;
            border-radius: 10%;
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
            color: red;
        }

        #datosPais {
            margin-left: auto;
            margin-right: auto;
            width: 100%;
            text-align: left;
            background-color: #a9cce3;
            border-radius: 10%;
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
