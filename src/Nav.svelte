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
                <span class="paises">PAÍSES</span>
            </Link>
        </li>
        <li class="item active">
            <Link to="/continentes">
                <span class="continentes">CONTINENTES</span>
            </Link>
        </li>
        <li class="item active">
            <Link to="/historico">
                <span class="historico">HISTÓRICO</span>
            </Link>
        </li>
    </ul>
</nav>

<!-- 👥 -->
<style>
    .navegador {
        background-color: #170a19;
        padding-top: 1px;
        padding-bottom: 1px;
        box-shadow: 0px 1px 10px grey;
        font-family: "Franklin Gothic Medium", "Arial Narrow", Arial, sans-serif;
    }
    .menu {
        display: flex;
        flex-direction: row;
        justify-content: space-evenly;
        text-decoration: none;
        list-style: none;
        padding: 15px;
    }
    .menu span {
        display: block;
        font-weight: bold;
        color: #a6d6d6;
    }

    .menu span:hover {
        color: #BC1333;
        transition: transform 0.2s linear;
        transform: scale(1.4);
    }
    
        @media (max-width: 425px) {
            .menu {
                padding: 10px;
            }
            .menu span {
                font-size: 12px;
            }
            .menu span:hover {
                color: #BC1333;
                transition: transform 0.2s linear;
                transform: scale(1.3);
            }
        }
    
</style>
