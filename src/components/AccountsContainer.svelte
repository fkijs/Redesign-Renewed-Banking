<script lang="ts">
    import AccountsList from "./Accounts/AccountsList.svelte";
    import AccountTransactionsList from "./Accounts/AccountTransactionsList.svelte";
    import { accounts } from '../store/stores';
    import { formatMoney } from "../utils/misc";
</script>

<div class="main">
    <section>
        <AccountsList />
        <AccountTransactionsList />
    </section>
    <h5><i class="fa-solid fa-wallet fa-fw"></i>{formatMoney($accounts[0].cash)}</h5>
</div>

<style>
    .main {
        overflow: hidden;
        width: 45%; /* Reducimos aún más el ancho */
        height: 75%; /* Ajustamos la altura */
        bottom: 12%; /* Centramos mejor */
        left: 27.5%; /* Ajustamos la posición */
        padding: 1rem; /* Espacio interior más generoso */
        position: absolute;
        /* Fondo con un gradiente elegante */
        background: radial-gradient(125% 125% at 50% 10%, #001f3f 30%, #001022 100%);
        border-radius: 12px; /* Bordes más redondeados */
        border: 2px solid rgba(255, 255, 255, 0.2); /* Bordes blancos más suaves */
        box-shadow: 0px 8px 24px rgba(0, 0, 0, 0.35); /* Sombra más definida */
    }

    section {
        display: flex;
        gap: 1rem; /* Reducimos un poco el gap entre las secciones */
        height: calc(100% - 2rem);
        color: #ffffff; /* Mantenemos el color del texto */
        background-color: rgba(0, 0, 0, 0.1); /* Fondo de sección ligeramente oscuro */
        padding: 0.5rem; /* Espaciado interno */
        border-radius: 8px; /* Bordes internos redondeados */
        box-shadow: inset 0 2px 5px rgba(0, 0, 0, 0.3); /* Sombra interna */
    }

    h5 {
        font-size: 1rem; /* Ajustamos el tamaño del texto */
        display: flex;
        align-items: center;
        gap: 0.4rem;
        position: absolute;
        bottom: 1rem;
        left: 1rem;
        color: #ffffff; /* Mantenemos el color del texto en blanco */
    }

    /* Añadimos un pequeño efecto hover a las secciones */
    .main:hover {
        border: 2px solid rgba(255, 255, 255, 0.3); /* Borde más marcado al pasar el mouse */
        box-shadow: 0px 10px 30px rgba(0, 0, 0, 0.4); /* Aumentamos la sombra */
        transition: all 0.3s ease;
    }
</style>