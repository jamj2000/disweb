<script>

    import { Route }  from "svelte-routing";
    import Inicio     from "./Inicio.svelte";
    import Paises  from "./Paises.svelte";
    import Continentes   from "./Continentes.svelte";
    import Historico   from "./Historico.svelte";

</script>


<main id="contenido">

    <Route path="/" component={Inicio} />
    <Route path="/paises" component={Paises} />
    <Route path="/continentes" component={Continentes} />
    <Route path="/historico" component={Historico} />

</main>