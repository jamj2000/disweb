<script>
    import { Link } from "svelte-routing";
</script>

<nav class="navegador">
    <ul class="menu">
        <li class="logo">
            <Link to="/">
                <span class="inicio">INICIO</span>
            </Link>
        </li>
        <li class="item active">
            <Link to="/paises">
                <span class="articulos">PAÍSES</span>
            </Link>
        </li>
        <li class="item active">
            <Link to="/continentes">
                <span class="clientes">CONTINENTES</span>
            </Link>
        </li>
        <li class="item active">
            <Link to="/historico">
                <span class="clientes">HISTÓRICO</span>
            </Link>
        </li>
    </ul>
</nav>

<!-- 👥 -->

<style>
    .navegador{
        background-color: #170a19;
        position: relative;
        top: 0;
        padding: 1px;
        box-shadow: 0px 1px 10px grey;
        font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;

    }
    .menu {
        display: flex;
        flex-direction: row;
        justify-content: space-evenly;
        text-decoration: none;
        list-style: none;
        padding: 15px;
    }
    .menu span{
        font-weight: bold;
        color: #a6d6d6;
    }
    .menu span:hover{
        color: #70416d ;
    }
    @media (max-width: 400px){
        .menu span{
            font-size: smaller;
        }
    }
</style>
