<script lang="ts">
    import { accounts, activeAccount, popupDetails, atm, translations } from "../../store/stores";
    import { formatMoney } from "../../utils/misc";
    export let account:any;

    function handleAccountClick(id: any) {
        activeAccount.update(() => id);
    };

    let isAtm: boolean;
    function handleButton(id:string, type:string) {
        let account = $accounts.find((accountItem: any) => id === accountItem.id);
        popupDetails.update(() => ({ actionType: type, account }));
    }

    atm.subscribe((usingAtm: boolean) => {
        isAtm = usingAtm;
    });
</script>

<section class="account" on:click={()=>handleAccountClick(account.id)} on:keydown={()=>{}}>
    <h4>
        {account.type}{$translations.account}/ {account.id}
    </h4>
    <h5>
        {account.type}{$translations.account}<br />
        <span>{account.name}</span>
    </h5>

    <div class="price">
        <strong>{formatMoney(account.amount)}</strong> <br />
        <span>{$translations.balance}</span>
    </div>

    <div class="btns-group">
        {#if !account.isFrozen}
            {#if !isAtm}
                <button class="btn btn-dark-green" on:click={() => handleButton(account.id, "deposit")}>{$translations.deposit_but}</button>
            {/if}
            <button class="btn btn-dark-orange" on:click={() => handleButton(account.id, "withdraw")}>{$translations.withdraw_but}</button>
            <button class="btn btn-dark-grey" on:click={() => handleButton(account.id, "transfer")}>{$translations.transfer_but}</button>
        {:else}
            <span class="frozen-text">{$translations.frozen}</span>
        {/if}
    </div>
</section>

<style>
    .account {
        background-color: #1c1c1c; /* Fondo oscuro para un look más profesional */
        padding: 0.8rem; /* Padding más pequeño para un diseño compacto */
        border-radius: 8px; /* Bordes redondeados para un diseño moderno */
        cursor: pointer;
        box-shadow: 0 4px 10px rgba(0, 0, 0, 0.3); /* Sombra más sutil */
        transition: transform 0.3s ease, box-shadow 0.3s ease;
    }

    .account:hover {
        transform: translateY(-2px); /* Efecto sutil al pasar el mouse */
        box-shadow: 0 8px 20px rgba(0, 0, 0, 0.4); /* Sombra más pronunciada al hover */
    }

    .account:not(:last-child) {
        margin-bottom: 1.2rem; /* Reducimos el espacio entre las cuentas */
    }

    h4 {
        font-size: 1.3rem; /* Ajustamos el tamaño del texto */
        color: #ffffff;
        margin-bottom: 0.4rem;
    }

    h5 {
        font-size: 1.1rem; /* Texto más pequeño */
        color: #b0b0b0;
    }

    h5 span {
        margin-top: 0.3rem;
        color: #dcdcdc; /* Color más claro para el nombre */
    }

    .price {
        text-align: right;
        margin-bottom: 1rem;
    }

    .price strong {
        font-size: 1.4rem; /* Texto más pequeño para el saldo */
        color: #ffffff;
    }

    .price span {
        color: #b0b0b0; /* Color más sutil para el balance */
    }

    .btns-group {
        display: grid;
        grid-template-columns: repeat(2, 1fr);
        grid-gap: 0.5rem;
    }

    .btn {
        padding: 0.6rem;
        border-radius: 5px;
        font-size: 0.9rem;
        font-weight: bold;
        cursor: pointer;
        transition: background-color 0.3s ease;
        border: none;
    }

    .btn-dark-green {
        background-color: #1c5d3f;
        color: white;
    }

    .btn-dark-green:hover {
        background-color: #164e33;
    }

    .btn-dark-orange {
        background-color: #a3572b;
        color: white;
    }

    .btn-dark-orange:hover {
        background-color: #8b471f;
    }

    .btn-dark-grey {
        background-color: #444444;
        color: white;
    }

    .btn-dark-grey:hover {
        background-color: #333333;
    }

    .frozen-text {
        color: #ff4c4c; /* Rojo claro para cuentas congeladas */
    }
</style>