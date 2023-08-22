<script>
    import { onMount } from 'svelte';

    let minutos = 25;
    let segundos = 0;
    let corriendo = false;
    let intervalo;
    let currentTrack = 1;
    const audioElement = new Audio(`audio/Lofi_${currentTrack}.mp3`);

    onMount(() => {
        audioElement.loop = false;
        audioElement.play();

        audioElement.addEventListener("ended", function() {
            currentTrack++;
            if (currentTrack > 12) {
                currentTrack = 1;
            }
            audioElement.src = `/audio/Lofi_${currentTrack}.mp3`;
            audioElement.play();
        });
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

    let volume = 1;
    let isPlaying = false;

    const adjustVolume = (e) => {
        volume = e.target.value / 100;
        audioElement.volume = volume;
    };

    const playPause = () => {
        if (audioElement.paused) {
            audioElement.play();
            isPlaying = true;
        } else {
            audioElement.pause();
            isPlaying = false;
        }
    }

    const nextTrack = () => {
        currentTrack++;
        if (currentTrack > 12) {
            currentTrack = 1;
        }
        audioElement.src = `/audio/Lofi_${currentTrack}.mp3`;
        audioElement.play();
    }

    const prevTrack = () => {
        currentTrack--;
        if (currentTrack < 1) {
            currentTrack = 12;
        }
        audioElement.src = `/audio/Lofi_${currentTrack}.mp3`;
        audioElement.play();
    }
</script>

<div class="text-center">
    <h2>{minutos}:{segundos < 10 ? '0' + segundos : segundos}</h2>
    <button class="btn btn-primary me-2" on:click={iniciar}>Iniciar</button>
    <button class="btn btn-warning me-2" on:click={detener}>Detener</button>
    <button class="btn btn-danger me-2" on:click={resetear}>Reiniciar</button>

    <div class="card glassmorphism">
        <div id="audio-controls" style="font-size: 2.5rem; color: #495057;">
            <i class="fa fa-step-backward" tabindex="0" on:click={prevTrack} on:keydown={(e) => { if(e.key === 'Enter' || e.key === ' ') prevTrack() }} style="cursor: pointer; margin: 0 20px;"></i>
            {#if isPlaying}
                <i class="fa fa-pause-circle" tabindex="0" on:click={playPause} on:keydown={(e) => { if(e.key === 'Enter' || e.key === ' ') playPause() }} style="cursor: pointer;"></i>
            {:else}
                <i class="fa fa-play-circle" tabindex="0" on:click={playPause} on:keydown={(e) => { if(e.key === 'Enter' || e.key === ' ') playPause() }} style="cursor: pointer;"></i>
            {/if}
            <i class="fa fa-step-forward" tabindex="0" on:click={nextTrack} on:keydown={(e) => { if(e.key === 'Enter' || e.key === ' ') nextTrack() }} style="cursor: pointer; margin: 0 20px;"></i>
        </div>
        <div id="volume" style="margin-top: 10px;">
            <span style="margin-right: 10px;">Volumen</span>
            <input type="range" min="0" max="100" value={volume * 100} on:input={adjustVolume} />
        </div>
    </div>
</div>

<style>

    i.fa {
        transition: 0.3s;
    }
    i.fa:hover {
        color: #007BFF;
        transform: scale(1.1);
    }
    i.fa:active {
        transform: scale(0.95);
    }
</style>
