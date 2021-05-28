<script>
    import { onMount } from "svelte";

    let value = "";
    var url = `https://disease.sh/v3/covid-19/countries/${value}`;
    var urlTodosLosPaises = `https://disease.sh/v3/covid-19/countries`;
    var urlVacuna = `https://disease.sh/v3/covid-19/vaccine/coverage/countries/${value}?lastdays=30&fullData=false`;

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
    let labelsMuertes = [];
    let dataMuertes = [];
    let labelsRecuperados = [];
    let dataRecuperados = [];

    let graficaCasos = new Chart();
    let graficaMuertes = new Chart();
    let graficaRecuperados = new Chart();

    function onChange() {
        fetch(`https://disease.sh/v3/covid-19/historical/${value}?lastdays=30`)
            .then((response) => response.json())
            .then((pais) => {
                console.log("PAIS: " + pais.country);
                casos = pais.timeline.cases;

                nombrePais = pais.country.toLowerCase;
                if (value.toLowerCase == nombrePais) {
                    //console.log(pais.timeline.cases);

                    //PRIMERA GRAFICA - CASOS

                    labelsCasos = Object.keys(pais.timeline.cases);
                    dataCasos = Object.values(pais.timeline.cases);
                    labelsCasos = labelsCasos
                        .map((x) => x.split("/"))
                        .map((x) => x[1] + "/" + x[0] + "/" + x[2]);

                    // INICIO GRAFICA

                    let ctxCasos = document
                        .getElementById("graficaCasos")
                        .getContext("2d");
                    graficaCasos.destroy();
                    graficaCasos = new Chart(ctxCasos, {
                        type: "line",
                        data: {
                            labels: labelsCasos,
                            datasets: [
                                {
                                    label: "Casos",
                                    borderColor: "#a58faa",
                                    hoverBorderColor: "#907fa4",
                                    pointColor: "#a6d6d6",
                                    pointStrokeColor: "#c1c7d1",
                                    pointHighlightFill: "#fff",
                                    pointHighlightStroke: "rgba(220,220,220,1)",
                                    data: dataCasos,
                                },
                            ],
                        },
                        options: {
                            responsive: true,
                            maintainAspectRatio: false,
                            scales: {
                                yAxes: [
                                    {
                                        stacked: true,
                                        gridLines: {
                                            display: true,
                                            color: "rgba(255,99,132,0.2)",
                                        },
                                    },
                                ],
                                xAxes: [
                                    {
                                        gridLines: {
                                            display: false,
                                        },
                                    },
                                ],
                            },
                        },
                    });

                    //FIN PRIMERA GRAFICA

                    //SEGUNDA GRAFICA - MUERTES

                    labelsMuertes = Object.keys(pais.timeline.deaths);
                    dataMuertes = Object.values(pais.timeline.deaths);
                    labelsMuertes = labelsMuertes
                        .map((x) => x.split("/"))
                        .map((x) => x[1] + "/" + x[0] + "/" + x[2]);

                    // INICIO GRAFICA

                    let ctx = document
                        .getElementById("graficaMuertes")
                        .getContext("2d");
                    graficaMuertes.destroy();
                    graficaMuertes = new Chart(ctx, {
                        type: "line",
                        data: {
                            labels: labelsMuertes,
                            datasets: [
                                {
                                    label: "Muertes",
                                    borderColor: "#F10808",
                                    hoverBorderColor: "green",
                                    pointColor: "rgba(210, 214, 222, 1)",
                                    pointStrokeColor: "#c1c7d1",
                                    pointHighlightFill: "#fff",
                                    pointHighlightStroke: "rgba(220,220,220,1)",
                                    data: dataMuertes,
                                },
                            ],
                        },
                        options: {
                            responsive: true,
                            maintainAspectRatio: false,
                            scales: {
                                yAxes: [
                                    {
                                        stacked: true,
                                        gridLines: {
                                            display: true,
                                            color: "rgba(255,99,132,0.2)",
                                        },
                                    },
                                ],
                                xAxes: [
                                    {
                                        gridLines: {
                                            display: false,
                                        },
                                    },
                                ],
                            },
                        },
                    });

                    //FIN SEGUNDA GRAFICA


                    //TERCERA GRAFICA - RECUPERADOS

                    labelsRecuperados = Object.keys(pais.timeline.recovered);
                    dataRecuperados = Object.values(pais.timeline.recovered);
                    labelsRecuperados = labelsRecuperados
                        .map((x) => x.split("/"))
                        .map((x) => x[1] + "/" + x[0] + "/" + x[2]);

                    // INICIO GRAFICA

                    let ctxRecuperados = document
                        .getElementById("graficaRecuperados")
                        .getContext("2d");
                    graficaRecuperados.destroy();
                    graficaRecuperados = new Chart(ctxRecuperados, {
                        type: "line",
                        data: {
                            labels: labelsRecuperados,
                            datasets: [
                                {
                                    label: "Recuperados",
                                    borderColor: "#c6ebc9",
                                    hoverBorderColor: "#907fa4",
                                    pointColor: "#70af85",
                                    pointStrokeColor: "#c1c7d1",
                                    pointHighlightFill: "#fff",
                                    pointHighlightStroke: "rgba(220,220,220,1)",
                                    data: dataRecuperados,
                                },
                            ],
                        },
                        options: {
                            responsive: true,
                            maintainAspectRatio: false,
                            scales: {
                                yAxes: [
                                    {
                                        stacked: true,
                                        gridLines: {
                                            display: true,
                                            color: "rgba(255,99,132,0.2)",
                                        },
                                    },
                                ],
                                xAxes: [
                                    {
                                        gridLines: {
                                            display: false,
                                        },
                                    },
                                ],
                            },
                        },
                    });
                }
            });

            fetch(`https://disease.sh/v3/covid-19/vaccine/coverage/countries/${value}?lastdays=30&fullData=false`)
            .then((response) => response.json())
            .then((vacuna) => { 


                
            });
    }
</script>

<select bind:value on:change={onChange} class="selectPais">
    {#each listaPaises as pais}
        <option value={pais}>{pais}</option>
    {/each}
</select>

<div class="contenedor">
    <div class="grafica">
        <canvas id="graficaCasos" height="400" width="400" />
    </div>
    <div class="grafica">
        <canvas id="graficaMuertes" height="400" width="400" />
    </div>
    <div class="grafica">
        <canvas id="graficaRecuperados" height="400" width="400" />
    </div>
</div>

<style>
    .selectPais{
        margin-top: 30px;
        width: 50%;
    }
    .contenedor {
        margin-top: 20px;
        display: flex;
        flex-direction: column;
        align-items: center;
        background-color: rgba(0, 0, 0, 0.528);
        width: 90%;
        margin-left: auto;
        margin-right: auto;
        border-radius: 1em;
        padding: 10px;
        padding-bottom: 20px;
        
    }
    .grafica {
        padding: 5px 15px 5px 15px;
        background-color: rgba(245, 245, 245, 0.802);
        width: 90%;
        max-height: 600px;
        margin: 10px;
        border-radius: 1em;
    }
    .grafica:hover {
        transition: transform 0.2s linear;
        transform: scale(1.1);
        box-shadow: 0px 1px 10px #BC1333;
    }
</style>
