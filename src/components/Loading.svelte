<section class="loading-container">
    <section class="loading-content">
        <div class="loading-spinner">
            <div></div>
            <div></div>
            <div></div>
            <div></div>
            <div></div>
            <div></div>
            <div></div>
            <div></div>
            <div></div>
            <div></div>
            <div></div>
            <div></div>
        </div>
    </section>
</section>

<style>
.loading-container {
    position: fixed;
    top: 0;
    left: 0;
    bottom: 0;
    right: 0;
    display: flex;
    align-items: center;
    justify-content: center;
    background-color: rgba(0, 0, 0, 0.5); /* Fondo oscuro con transparencia */
    z-index: 1000; /* Asegura que esté siempre en el frente */
}

.loading-content {
    max-width: 40rem;
    max-height: 20rem;
    width: 100%;
    height: 100%;
    background-color: #1c1c1c; /* Fondo oscuro */
    padding: 3rem;
    border-radius: 1rem;
    display: flex;
    align-items: center;
    justify-content: center;
    box-shadow: 0 8px 16px rgba(0, 0, 0, 0.25); /* Sombra suave */
    animation: fade-in 0.5s ease-in-out;
}

.loading-spinner {
    display: inline-block;
    position: relative;
    width: 80px;
    height: 80px;
}

.loading-spinner div {
    transform-origin: 40px 40px;
    animation: loading-spinner 1.2s linear infinite;
}

.loading-spinner div:after {
    content: " ";
    display: block;
    position: absolute;
    top: 3px;
    left: 37px;
    width: 6px;
    height: 18px;
    border-radius: 20%;
    background: #ffffff; /* Color blanco para las barras */
    box-shadow: 0px 0px 10px rgba(255, 255, 255, 0.8); /* Efecto de luz suave */
}

.loading-spinner div:nth-child(1) {
    transform: rotate(0deg);
    animation-delay: -1.1s;
}
.loading-spinner div:nth-child(2) {
    transform: rotate(30deg);
    animation-delay: -1s;
}
.loading-spinner div:nth-child(3) {
    transform: rotate(60deg);
    animation-delay: -0.9s;
}
.loading-spinner div:nth-child(4) {
    transform: rotate(90deg);
    animation-delay: -0.8s;
}
.loading-spinner div:nth-child(5) {
    transform: rotate(120deg);
    animation-delay: -0.7s;
}
.loading-spinner div:nth-child(6) {
    transform: rotate(150deg);
    animation-delay: -0.6s;
}
.loading-spinner div:nth-child(7) {
    transform: rotate(180deg);
    animation-delay: -0.5s;
}
.loading-spinner div:nth-child(8) {
    transform: rotate(210deg);
    animation-delay: -0.4s;
}
.loading-spinner div:nth-child(9) {
    transform: rotate(240deg);
    animation-delay: -0.3s;
}
.loading-spinner div:nth-child(10) {
    transform: rotate(270deg);
    animation-delay: -0.2s;
}
.loading-spinner div:nth-child(11) {
    transform: rotate(300deg);
    animation-delay: -0.1s;
}
.loading-spinner div:nth-child(12) {
    transform: rotate(330deg);
    animation-delay: 0s;
}

@keyframes loading-spinner {
    0% {
        opacity: 1;
    }
    100% {
        opacity: 0;
    }
}

@keyframes fade-in {
    from {
        opacity: 0;
    }
    to {
        opacity: 1;
    }
}

</style>
