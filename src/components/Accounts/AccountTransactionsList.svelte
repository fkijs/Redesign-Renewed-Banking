<script lang="ts">
    import { accounts, activeAccount, translations, atm, notify } from "../../store/stores";
    import AccountTransactionItem from "./AccountTransactionItem.svelte";
    import { convertToCSV } from "../../utils/convertToCSV";
    import { setClipboard } from "../../utils/setClipboad";
    
    let transSearch = '';
    $: account = $accounts.find((accountItem: any) => $activeAccount === accountItem.id);

    function handleClickExportData() {
        if (account == null) console.log("No account selected");
        if (account.transactions.length === 0) {
            notify.set("No transactions to export!");
            setTimeout(() => {
                notify.set("");
            }, 3500);
            return;
        }
        const csv = convertToCSV(account.transactions);
        setClipboard(csv);
        notify.set("Datos copiados en el portapapeles!");
        setTimeout(() => {
            notify.set("");
        }, 3500);
    }

    let isAtm: boolean = false;
    atm.subscribe((usingAtm: boolean) => {
        isAtm = usingAtm;
    });
</script>

<section class="transactions-container">
    <h3 class="heading">
        <span>{$translations.transactions}</span>
        <div>
            <img src="./img/bank.png" alt="bank icon" />
            <span>{$translations.bank_name}</span>
        </div>
    </h3>

    <input type="text" class="transactions-search" placeholder={$translations.trans_search} bind:value={transSearch}>

    <section class="scroller">
        {#if account}
            {#if account.transactions.filter(item => item.message.toLowerCase().includes(transSearch.toLowerCase()) || item.trans_id.toLowerCase().includes(transSearch.toLowerCase()) || item.receiver.toLowerCase().includes(transSearch.toLowerCase())).length > 0}
                {#each account.transactions.filter(item => item.message.toLowerCase().includes(transSearch.toLowerCase()) || item.trans_id.toLowerCase().includes(transSearch.toLowerCase()) || item.receiver.toLowerCase().includes(transSearch.toLowerCase())) as transaction (transaction.trans_id)}
                    <AccountTransactionItem {transaction} />
                {/each}
            {:else}
                <h3 class="no-transactions">{$translations.trans_not_found}</h3>
            {/if}
        {:else}
            {$translations.select_account}
        {/if}
    </section>

    {#if !isAtm}
        <div class="export-data">
            <button class="btn btn-green" on:click|preventDefault={handleClickExportData}>
                <i class="fa-solid fa-file-export fa-fw" />
                {$translations.export_data}
            </button>
        </div>
    {/if}
</section>

<style>
    .transactions-container {
        flex: 1 1 45%; /* Compactamos un poco más el ancho */
        padding: 0.5rem;
        background-color: #1a1a1a; /* Fondo oscuro y limpio */
        border-radius: 10px; /* Bordes más redondeados */
        box-shadow: 0 6px 15px rgba(0, 0, 0, 0.3); /* Sombra suave */
        color: #e0e0e0;
        max-width: 650px; /* Limita el ancho máximo */
    }

    .heading {
        display: flex;
        justify-content: space-between;
        margin-bottom: 0.5rem;
        font-size: 1.1rem;
        color: #ffffff;
        font-weight: bold;
    }

    .heading div {
        display: flex;
        align-items: center;
    }

    .heading img {
        width: 1.8rem;
        margin-right: 0.5rem;
    }

    .transactions-search {
        width: 100%;
        border-radius: 5px;
        border: 1px solid #444;
        padding: 0.8rem; /* Ajustamos el padding */
        margin-bottom: 1rem;
        background-color: #292929; /* Fondo ligeramente más claro */
        color: #ffffff;
        font-size: 1rem;
        box-shadow: inset 0 2px 4px rgba(0, 0, 0, 0.2);
        transition: border-color 0.3s ease;
    }

    .transactions-search:focus {
        border-color: #007bff;
        outline: none;
    }

    .scroller {
        max-height: 35vh; /* Más compacto */
        overflow-y: auto;
        padding-right: 1rem;
    }

    .no-transactions {
        text-align: left;
        color: #f3f4f5;
        margin-top: 0.5rem;
        font-size: 1rem;
    }

    .export-data {
        margin-top: 0.5rem;
        display: flex;
        justify-content: flex-end;
    }

    .btn {
        display: flex;
        align-items: center;
        justify-content: center;
        gap: 0.75rem;
        padding: 0.6rem 1.2rem;
        border: none;
        border-radius: 5px;
        font-size: 0.9rem;
        font-weight: bold;
        cursor: pointer;
        transition: background-color 0.3s ease, transform 0.2s ease;
        color: white;
        box-shadow: 0 4px 10px rgba(0, 0, 0, 0.2);
    }

    .btn-green {
        background-color: #28a745;
    }

    .btn-green:hover {
        background-color: #218838;
        transform: scale(1.05);
    }
</style>