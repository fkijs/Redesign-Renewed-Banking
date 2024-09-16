<script>
    import { notify } from "../store/stores";
</script>

<section class="notification-container">
    <section class="notification-content">
        <i class="start-icon fa fa-info-circle fa-2x"></i>
        <strong class="notification-text">{$notify}</strong> 
    </section>
</section>

<style>
    .notification-container {
        width: 20%; /* Más ancho para permitir más texto */
        box-sizing: border-box;
        padding: 10px 8px;
        margin: 10px 0px;
        position: absolute;
        left: 5%;
        top: 4%;
        z-index: 1000; /* Asegura que esté visible por encima de otros elementos */
        animation: slide-in 0.5s ease-out;
    }

    .notification-content {
        background-color: #1c1c1c; /* Fondo oscuro */
        color: #ffffff; /* Texto blanco */
        padding: 1rem 1.5rem; /* Más espaciado interno */
        border-radius: 1rem; /* Bordes redondeados */
        display: flex;
        align-items: center;
        box-shadow: 0 4px 10px rgba(0, 0, 0, 0.3); /* Sombra suave */
        font-size: 1rem;
        transition: transform 0.3s ease, opacity 0.3s ease; /* Transición suave */
    }

    .start-icon {
        color: #007bff; /* Color azul para el ícono */
        margin-right: 10px; /* Separación entre el ícono y el texto */
    }

    .notification-text {
        font-size: 1.1rem; /* Tamaño ajustado del texto */
        font-weight: bold;
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
</style>
