<script>
    import { onMount } from "svelte";

    let value = "";
    var url = `https://disease.sh/v3/covid-19/countries/${value}`;
    var urlTodosLosPaises = `https://disease.sh/v3/covid-19/countries`;

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

    let graficaCasos = new Chart();
    let graficaMuertes = new Chart();
    let graficaRecuperados = new Chart();

    function onChange() {
        fetch(`https://disease.sh/v3/covid-19/historical/${value}?lastdays=35`)
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

                    //PRIMERA GRAFICA - MUERTES

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
                        },
                    });

                    //FIN PRIMERA GRAFICA
                }
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
</div>

<style>
    .contenedor {
        display: flex;
        flex-direction: column;
        align-items: center;
        background-color: rgba(245, 245, 245, 0.604);
        width: 90%;
        margin-left: auto;
        margin-right: auto;
        border-radius: 1em;
        padding: 10px;
    }
    .grafica {
        padding: 5px 15px 5px 15px;
        background-color: rgba(245, 245, 245, 0.604);
        width: 90%;
        max-height: 600px;
        margin: 10px;
    }
</style>
