<script lang="ts">
    import { accounts, translations } from "../../store/stores";
    import AccountListItem from "./AccountListItem.svelte";
    let accSearch = "";
</script>

<aside>
    <h3 class="heading">{$translations.accounts}</h3>
    <input type="text" class="acc-search" placeholder={$translations.account_search} bind:value={accSearch} />
    <section class="scroller">
        {#if $accounts.filter(item => item.name.toLowerCase().includes(accSearch.toLowerCase())).length > 0}
            {#each $accounts.filter(item => item.name.toLowerCase().includes(accSearch.toLowerCase())) as account (account.id)}
                <AccountListItem {account} />
            {/each}
        {:else}
            <h3 style="text-align: left; color: #F3F4F5; margin-top: 1rem;">{$translations.account_not_found}</h3>
        {/if}
    </section>
</aside>

<style>
    aside {
        flex: 0 0 23%; /* Reducimos el ancho del aside */
        padding-left: 0.8rem; /* Ajustamos el padding */
        padding-top: 0.5rem;
        background-color: #1c1c1c; /* Fondo oscuro para mantener la coherencia */
        border-radius: 8px; /* Bordes más redondeados */
        box-shadow: 0 4px 12px rgba(0, 0, 0, 0.2); /* Sombra suave */
    }

    .heading {
        color: #ffffff; /* Texto blanco para el título */
        font-size: 1.3rem; /* Tamaño de fuente más pequeño */
        margin-bottom: 1rem;
        text-align: center; /* Centramos el título */
    }

    .acc-search {
        width: 100%;
        border-radius: 5px;
        border: none;
        padding: 1rem; /* Reducimos el padding */
        margin-bottom: 1rem;
        background-color: #2a2a2a; /* Fondo oscuro para el input */
        color: #ffffff; /* Texto blanco */
        box-shadow: inset 0 2px 4px rgba(0, 0, 0, 0.2); /* Sombra interna para darle profundidad */
        font-size: 1rem; /* Tamaño de fuente más pequeño */
    }

    .acc-search::placeholder {
        color: #b0b0b0; /* Color para el placeholder */
    }

    .scroller {
        height: 80vh; /* Ajustamos la altura de la lista */
        overflow-y: auto; /* Hacemos que la lista sea desplazable */
        padding-right: 0.5rem;
    }

    /* Estilo para cuando no se encuentra una cuenta */
    h3 {
        color: #f1f1f1; /* Color sutil para el mensaje */
        font-size: 1.1rem;
    }
</style>