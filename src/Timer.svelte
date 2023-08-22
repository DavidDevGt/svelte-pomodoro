<script>
    import { onMount } from 'svelte';

    let minutos = 25;
    let segundos = 0;
    let corriendo = false;
    let intervalo;

    onMount(() => {
        // Cargar el lofi yt
        const audioElement = new Audio("URL_LOFI");
        audioElement.loop = true;
        audioElement.play();
    });

    const iniciar = () => {
        corriendo = true;
        intervalo = setInterval(contar, 1000);
    }

    const detener = () => {
        corriendo = false;
        clearInterval(intervalo);
    }

    const resetear = () => {
        detener();
        minutos = 25;
        segundos = 0;
    }

    const contar = () => {
        if (segundos === 0) {
            if (minutos === 0) {
                detener();
                alert('Tiempo de descanso');
            } else {
                minutos--;
                segundos = 59;
            }
        } else {
            segundos--;
        }
    };
</script>

<div class="text-center">
    <h2>{minutos}:{segundos < 10 ? '0' + segundos : segundos}</h2>
    <button class="btn btn-primary me-2" on:click={iniciar}>Iniciar</button>
    <button class="btn btn-warning me-2" on:click={detener}>Detener</button>
    <button class="btn btn-danger me-2" on:click={resetear}>Resetear</button>
</div>