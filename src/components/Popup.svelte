<script lang="ts">
    import { accounts, activeAccount, popupDetails, loading, translations } from "../store/stores";
    import {fetchNui} from "../utils/fetchNui"
    let amount: number = 0;
    let comment: string = "";
    let stateid: string = "";
    $: account = $accounts.find((accountItem: any) => $activeAccount === accountItem.id);

    function closePopup() {
        popupDetails.update((val: any) => ({
            ...val,
            actionType: ""
        }));
    }

    function submitInput() {
        loading.set(true);
        fetchNui($popupDetails.actionType, {fromAccount: $popupDetails.account.id, amount: amount, comment: comment, stateid: stateid}).then(retData => {
            setTimeout(() => {
                if (retData !== false){
                    accounts.set(retData);
                }
                loading.set(false);
            }, 1000);
        })
        closePopup();
    }
</script>

<section class="popup-container">
    <section class="popup-content">
        <h2> {$popupDetails.account.type}{$translations.account}/ {$popupDetails.account.id}</h2>
        <form action="#">
            <div class="form-row">
                <label for="amount">{$translations.amount}</label>
                <input bind:value={amount} type="number" name="amount" id="amount" placeholder="$" />
            </div>

            <div class="form-row">
                <label for="comment">{$translations.comment}</label>
                <input bind:value={comment} type="text" name="comment" id="comment" placeholder="//" />
            </div>

            {#if $popupDetails.actionType === "transfer"}
                <div class="form-row">
                    <label for="stateId">{$translations.transfer}</label>
                    <input bind:value={stateid} type="text" name="stateId" id="stateId" placeholder="#" />
                </div>
            {/if}

            <div class="btns-group">
                <button type="button" class="btn btn-orange" on:click={closePopup}>{$translations.cancel}</button>
                <button type="button" class="btn btn-green" on:click={() => submitInput()}>{$translations.confirm}</button>
            </div>
        </form>
    </section>
</section>

<style>
    .popup-container {
        position: fixed;
        top: 0;
        left: 0;
        bottom: 0;
        right: 0;
        background-color: rgba(0, 0, 0, 0.7); /* Fondo oscuro con opacidad */
        display: flex;
        align-items: center;
        justify-content: center;
        z-index: 1000;
        animation: fade-in 0.5s ease-in-out; /* Animación de entrada */
    }

    .popup-content {
        max-width: 35rem;
        width: 100%;
        background-color: #1c1c1c; /* Fondo oscuro */
        padding: 2.5rem;
        border-radius: 0.8rem;
        box-shadow: 0 8px 20px rgba(0, 0, 0, 0.5); /* Sombra suave */
        color: #ffffff; /* Texto blanco */
        animation: slide-in 0.5s ease-out; /* Animación de entrada */
        font-family: 'Roboto', sans-serif;
    }

    h2 {
        margin-bottom: 1.5rem;
        text-align: center;
        font-size: 1.8rem;
        font-weight: bold;
        color: #ffffff; /* Título en blanco */
    }

    .form-row {
        display: flex;
        flex-direction: column;
        gap: 1rem;
        margin-bottom: 1.5rem;
    }

    .form-row label {
        font-size: 1.1rem;
        color: #cccccc; /* Gris claro para los labels */
    }

    .form-row input {
        width: 100%;
        border-radius: 0.5rem;
        background-color: #2b2b2b; /* Fondo más oscuro para inputs */
        border: 1px solid #444; /* Borde gris oscuro */
        padding: 0.8rem;
        color: #ffffff; /* Texto blanco */
        font-size: 1.2rem;
        box-shadow: inset 0 2px 4px rgba(0, 0, 0, 0.2); /* Sombra interna */
        transition: border 0.3s ease;
    }

    .form-row input:focus {
        border-color: #007bff; /* Azul más definido al enfocar */
        outline: none;
    }

    .btns-group {
        display: flex;
        justify-content: space-between;
        margin-top: 2rem;
    }

    .btn {
        padding: 0.8rem 1.5rem;
        border: none;
        border-radius: 0.5rem;
        font-size: 1.1rem;
        font-weight: bold;
        cursor: pointer;
        transition: background-color 0.3s ease, transform 0.2s ease; /* Suave transición */
        color: white;
        box-shadow: 0 4px 10px rgba(0, 0, 0, 0.2); /* Sombra para el botón */
    }

    .btn-orange {
        background-color: #e67e22; /* Naranja */
    }

    .btn-orange:hover {
        background-color: #d35400; /* Naranja más oscuro en hover */
        transform: scale(1.05); /* Efecto de agrandado */
    }

    .btn-green {
        background-color: #28a745; /* Verde para confirmar */
    }

    .btn-green:hover {
        background-color: #218838; /* Verde más oscuro en hover */
        transform: scale(1.05); /* Efecto de agrandado */
    }

    /* Animación de entrada */
    @keyframes slide-in {
        0% {
            transform: translateY(-20px);
            opacity: 0;
        }
        100% {
            transform: translateY(0);
            opacity: 1;
        }
    }

    /* Animación de desvanecimiento */
    @keyframes fade-in {
        0% {
            background-color: rgba(0, 0, 0, 0);
        }
        100% {
            background-color: rgba(0, 0, 0, 0.7);
        }
    }
</style>