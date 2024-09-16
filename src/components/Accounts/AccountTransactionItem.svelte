<script lang="ts">
    export let transaction: any;
    import { formatMoney } from "../../utils/misc";
    import { translations } from "../../store/stores";
    function getTimeElapsed(seconds: number): string {
        let retData: string;
        const timestamp = Math.floor(Date.now() / 1000)-seconds;
        const minutes = Math.floor(timestamp / 60);
        const hours = Math.floor(minutes / 60);
        const days = Math.floor(hours / 24);
        const weeks = Math.floor(days / 7);

        if (weeks !== 0 && weeks > 1) {
            retData = $translations.weeks.replace("%s", weeks);
        } else if (weeks !== 0 && weeks === 1) {
            retData = $translations.aweek;
        } else if (days !== 0 && days > 1) {
            retData = $translations.days.replace("%s", days);
        } else if (days !== 0 && days === 1) {
            retData = $translations.aday;
        } else if (hours !== 0 && hours > 1) {
            retData = $translations.hours.replace("%s", hours);
        } else if (hours !== 0 && hours === 1) {
            retData = $translations.ahour;
        } else if (minutes !== 0 && minutes > 1) {
            retData = $translations.mins.replace("%s", minutes);
        } else if (minutes !== 0 && minutes === 1) {
            retData = $translations.amin;
        } else {
            retData = $translations.secs;
        }
        return retData;
    }
</script>

<section class="transaction">
    <h5>
        <span class="title-container" class:withdrawTitle={transaction.trans_type === "withdraw"}>
            {transaction.title}
            <p>[{transaction.trans_type.toUpperCase()}]</p>
        </span>
        <span class="trans_id" class:withdrawId={transaction.trans_type === "withdraw"}>{transaction.trans_id}</span>
    </h5>
    <h4>
        <div class="amount-section">
            <span class:withdraw={transaction.trans_type === "withdraw"}>
                <i class="fa-solid fa-money-bill"></i>
                {formatMoney(transaction.amount)}
            </span>
        </div>
        <div class="receiver-info">
            <span> {transaction.receiver} </span>
            <span>{getTimeElapsed(transaction.time)} <br /> {transaction.issuer}</span>
        </div>
    </h4>

    <h6>
        <strong>{$translations.message}</strong> <br />
        {transaction.message}
    </h6>
</section>

<style>
    .transaction {
        background-color: #212529; /* Fondo más oscuro para integrarse con el resto del diseño */
        padding: 1.2rem;
        border-radius: 8px;
        font-size: 1.2rem;
        font-weight: 400;
        border: 1px solid #343a40; /* Borde sutil */
        box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1); /* Sombra ligera para darle profundidad */
        transition: transform 0.3s ease, box-shadow 0.3s ease;
        color: #f1f1f1;
    }

    .transaction:not(:last-child) {
        margin-bottom: 1.5rem;
    }

    .transaction:hover {
        transform: scale(1.01);
        box-shadow: 0 8px 16px rgba(0, 0, 0, 0.15);
    }

    .title-container {
        display: flex;
        align-items: center;
        gap: 0.6rem;
    }

    .title-container > p {
        background-color: #28a745; /* Verde para transacciones exitosas */
        color: white;
        padding: 0.4rem 0.8rem;
        border-radius: 6px;
    }

    .title-container.withdrawTitle > p {
        background-color: #dc3545; /* Rojo para retiros */
        color: white;
    }

    .trans_id {
        background-color: #6c757d; /* Gris suave */
        color: #f1f1f1;
        padding: 0.3rem 1rem;
        border-radius: 6px;
        font-size: 0.9rem;
    }

    .trans_id.withdrawId {
        background-color: #dc3545; /* Rojo para retiros */
        color: white;
    }

    .transaction h5 {
        display: flex;
        justify-content: space-between;
        padding-bottom: 0.5rem;
        margin-bottom: 1rem;
        border-bottom: 2px solid #495057;
    }

    .transaction h4 {
        display: flex;
        justify-content: space-between;
        align-items: flex-start;
        font-size: 1.2rem;
        color: #adb5bd;
    }

    .amount-section {
        display: flex;
        flex-direction: column;
        align-items: flex-start;
    }

    .transaction h4 span:first-child {
        font-size: 1.5rem;
        color: #28a745; /* Verde para depósitos */
    }

    .transaction h4 span.withdraw {
        color: #dc3545; /* Rojo para retiros */
    }

    .receiver-info {
        display: flex;
        flex-direction: column;
        text-align: right;
        color: #ced4da;
    }

    .receiver-info span {
        font-size: 1rem;
        margin-top: 0.2rem;
    }

    .transaction h6 {
        color: #adb5bd;
        margin: 1.2rem 0 1.5rem;
        font-size: 1rem;
    }

    .transaction h6 strong {
        color: #f8f9fa;
        font-weight: 500;
    }
</style>