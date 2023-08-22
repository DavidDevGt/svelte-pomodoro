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

    const = iniciar = () => {
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
        if
    }
</script>