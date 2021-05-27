<script>
</script>

<h1>BIENVENIDOS A INFOCOVID</h1>

<div>
    <h2 class="subtitulo">¿Que veremos en esta web?</h2>
    <div class="queVeremos">
        <div class="contenidoPaises divIndividual">
            <h2 class="subtituloDiv">Informacion relacionada con los países</h2>
            <p class="parrafoDiv">
                En la <span class="mayusculas "> sección </span>  <span class="mayusculas negrita">Países </span> veremos información detallada sobre los
                casos de <span class="mayusculas negrita cursiva">Covid-19</span> en tiempo real. 
                <br /><br />
                 
                Datos como los casos, las muertes y los recuperados que ha tenido cada país desde que comenzó la pandemia así como los tests realizados, e incluso
                las cifras que se manejan cada día, que se actualizarán cada 10 minutos.

                <br><br />
                Además tendremos la información de las tasas por cada millon de habitantes de los tests realizados, los casos, el número de personas en estado grave,
                las muertes y los recuperados.
               
                
                <br /><br />
                Para mayor información se incluirán detalles como la bandera de cada país y sus coordenadas geográficas.
            </p>
        </div>

        <div class="contenidoContinentes divIndividual">
            <h2 class="subtituloDiv">Informacion relacionada con los continentes</h2>
            <p class="parrafoDiv">
                En la <span class="mayusculas "> sección </span>  <span class="mayusculas negrita">continentes </span> veremos información detallada sobre los
                casos de <span class="mayusculas negrita cursiva">Covid-19</span> en tiempo real. 
                <br /><br />
                 
                Aquí podremos ver los casos, las muertes y los recuperados que ha tenido cada continente desde que comenzó la pandemia así como los tests realizados, e incluso
                las cifras que se manejan cada día, que se actualizarán cada 10 minutos.

                <br><br />
                Además tendremos la información de las tasas por cada millon de habitantes de los tests realizados, los casos, el número de personas en estado grave,
                las muertes y los recuperados.
               
                
                <br /><br />
                También incluiremos las coordenadas geográficas de cada continente.
            </p>
        </div>

        <div class="contenidoHistorico divIndividual">
            <h2 class="subtituloDiv">Datos historicos sobre el Covid</h2>
            <p class="parrafoDiv">
                En la <span class="mayusculas "> sección </span>  <span class="mayusculas negrita">histórico </span> veremos graficas con los datos de los ultimos
                30 días sobre el covid en cada país. <br />
                En estas graficas veremos los datos sobre los casos, muertes y recuperaciones.
            </p>
        </div>
    </div>
    <div class="divAgradecimiento">
        <h4>
            Todo ello ha sido posible gracias a la api
            <a href="https://www.disease.sh" target="blank">disease.sh </a>
            y a la web de donde extrae la información
            <a href="https://www.worldometers.info/" target="blank"
                >Worldometer</a
            >.
        </h4>
    </div>
</div>
<footer class="footer">
    <div class="informaciónAlumno">
        <p>
            Esta web ha sido elaborada por Juan Manuel Fernández Velarde, alumno
            del I.E.S Luis Vélez de Guevara como proyecto de fin de grado para
            el CFGS de Desarrollo de Aplicaciones Web
        </p>
    </div>
    <div class="redes">
        <h3>Redes sociales:</h3>
        <ul class="listaRedes">
            <li>
                <a
                    href="https://www.linkedin.com/in/juanmanuelfernandezvelarde/"
                    target="blank"
                    class="enlaceFooter"
                >
                    <img
                        src="/images/icons/linkedin.png"
                        alt="logoLinkedIn"
                        class="logoRedes logoLinkedin"
                    />  LinkedIn</a
                >
            </li>
            <li>
                <a
                    href="https://www.instagram.com/juanmaferv96"
                    target="blank"
                    class="enlaceFooter"
                >
                    <img
                        src="/images/icons/instagram.png"
                        alt="logoLinkedIn"
                        class="logoRedes"
                    /> Instagram</a
                >
            </li>
            <li>
                <a
                    href="https://www.twitter.com/juanmaferv96"
                    target="blank"
                    class="enlaceFooter"
                >
                    <img
                        src="/images/icons/twitter.png"
                        alt="logoLinkedIn"
                        class="logoRedes"
                    /> Twitter</a
                >
            </li>
        </ul>
    </div>
</footer>

<style>
    @font-face{
        font-family: Bevan;
        src:url("/fonts/Bevan-Regular.ttf");
    }
    :global(body) {
        
        background-image: url("/images/icons/covid.jpg");
    }

    * {
        font-family: "Franklin Gothic Medium", "Arial Narrow", Arial, sans-serif;
    }

    h1 {
        display: flex;
        height: 200px;
        padding-top: 8px;
        margin: 0;
        flex-wrap: nowrap;
        justify-content: center;
        align-items: center;
        color: black;
        font-family: Bevan;
        background-color: #ededd08c;
        font-size: 50px;
    }
    .subtitulo {
        
        color: black;
        padding: 1%;
        background-color: rgba(255, 235, 205, 0.694);
    }
    .queVeremos {
        font-family: "Franklin Gothic Medium", "Arial Narrow", Arial, sans-serif;
        display: flex;
        color: black;
        flex-direction: row;
        flex-wrap: wrap;
        justify-content: space-around;
        align-items: center;
    }
    .divIndividual {
        font-family: "Franklin Gothic Medium", "Arial Narrow", Arial, sans-serif;
        background-color: rgba(255, 255, 255, 0.686);
        border-radius: 0;
        padding: 1%;
        max-width: 30%;
        min-height: 500px;
        text-align: justify;
        
    }
    .subtituloDiv{
        text-align: center;
        height: 50px;
        padding-bottom: 10px;
        border-bottom: 1px solid black;
    }
    .mayusculas{
        text-transform: uppercase;
    }
    .negrita{
        font-weight: bold;
    }
    .cursiva{
        font-style: italic;
    }
    .divAgradecimiento {
        max-width: 98%;
        width: 98%;
        margin-left: auto;
        margin-right: auto;
        background-color: rgba(255, 255, 255, 0.686);
        padding: 5px;
        margin-top: 15px;
        border-radius: 0;
        color: black;
    }
    .footer {
        background-color: black;
        padding-bottom: 1px;
    }
    .informaciónAlumno {
        color: white;
        margin-top: 10px;
        padding-top: 10px;
        text-align: center;
    }
    .redes {
        color: white;
    }
    ul {
        list-style: none;
    }
    .listaRedes {
        padding: 0;
        display: flex;
        justify-content: space-evenly;
        flex-wrap: wrap;
    }
    .logoRedes {
        
        width: 30px;
    }
    .logoLinkedin{
        padding-right: 2px;
    }
    .enlaceFooter {
        display: flex;
        flex-direction: row;
        flex-wrap: nowrap;
        align-items: center;
    }

    @media (max-width: 1024px) {
        h1{
            font-size: 35px;
        }
        .divIndividual {
            font-size: 14.5px;
        }
        .divAgradecimiento {
            font-size: small;
        }
        .informaciónAlumno {
            font-size: small;
        }
    }

    @media (max-width: 768px) {
        h1{
            font-size: 25px;
        }
        .divIndividual {
            font-size: x-small;
            min-height: 300px;
        }
        .divAgradecimiento {
            font-size: small;
        }
        .informaciónAlumno {
            font-size: small;
        }
        .subtituloDiv{
        text-align: center;
        height: 30px;
        padding-bottom: 10px;
        border-bottom: 1px solid black;
    }
    }
    @media (max-width: 600px) {

        .queVeremos {
            flex-direction: column;
            align-items: center;
        }
        .divIndividual {
            font-size: x-small;
            max-width: 90%;
            min-height: 200px;
            width: 90%;
            margin-bottom: 10px;
        }
        .parrafoDiv{
            padding: 5px;
        }
        .divAgradecimiento {
            font-size: 10px;
            max-width: 90%;
            width: 90%;
        }
        .informaciónAlumno {
            font-size: xx-small;
        }
        .redes {
            font-size: small;
        }
    }
    @media (max-width: 400px) {
        h1{
            height: 150px;
        }

        }
</style>
