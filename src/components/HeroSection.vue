<script setup lang="ts">

</script>

<template>
    <div class="wrapper">
        <div class="content">
            <h1>Brug for nogle at snakke med? <br />Vi står klar til at hjælpe</h1>
            <p>7 Kopper står til rådighed og forbinder dig med en empatisk lytter, der tilbyder gratis støtte.</p>
            <button @click="'https://7kopper.dk/mentor'">Kickstart din rejse</button>
            <p>Til dig, der har brug for støtte – uden at det koster</p>
        </div>
        <div class="container-flex">
            <div class="content-flex">
                <img alt="Vue logo" class="logo" src="/images/1on1.png" width="64" height="64" />
                <div>
                    <h2>Kaffemøder</h2>
                    <p>Personlig samtale – gratis støtte til dig, der har brug for nogen at tale med, uden økonomisk
                        pres.
                    </p>
                </div>
            </div>
            <div class="content-flex">
                <img alt="Vue logo" class="logo" src="/images/remote-talk.png" width="64" height="64" />
                <div>
                    <h2>Videochat</h2>
                    <p>Støtte over telefon eller video – gratis samtale, hvor du er, når du har brug for det.</p>
                </div>
            </div>
            <div class="content-flex">
                <img alt="Vue logo" class="logo" src="/images/walk-and-talk.png" width="64" height="64" />
                <div>
                    <h2>Ude i naturen</h2>
                    <p>En samtale i naturen – rolig støtte i frisk luft, med plads til dine tanker og følelser.</p>
                </div>
            </div>
        </div>
        <div class="video-background">
            <video autoplay muted loop playsinline>
                <source src="/videos/drinking.mp4" type="video/mp4">
            </video>
            <div class="overlay"></div>

        </div>
    </div>
</template>

<style scoped>
.content {
    display: flex;
    flex-direction: column;
    color: var(--kopper-beige);
    text-align: left;
    gap: 0.5rem;
}

.container-flex {
    display: flex;
    flex-direction: column;
    align-items: start;
    justify-content: start;
    gap: 1rem;

    h2 {
        font-size: 1.5rem;
        font-weight: bold;
        margin: 0;
        color: var(--kopper-beige);
    }

    p {
        font-size: 1rem;
        color: var(--kopper-beige);
    }
}

.content-flex {
    display: flex;
    flex-direction: row;
    align-items: start;
    justify-content: center;
    gap: 10px;
}

.wrapper {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: space-evenly;
    height: 100%;
    margin: 0 auto;
}

button {
    background-color: var(--kopper-lilac);
    color: var(--kopper-dark-text);
    padding: 0.8rem 1.4rem;
    margin: 1rem 0;
    border: none;
    border-radius: 12px;
    font-size: 1rem;
    font-family: inherit;
    font-weight: bold;
    cursor: pointer;
    transition: background-color 0.3s ease, transform 0.2s ease;
    box-shadow: 0 2px 6px rgba(0, 0, 0, 0.08);
    width: fit-content;
}

button:hover {
    background-color: color-mix(in srgb, var(--color-accent) 90%, #ffffff 10%);
    transform: translateY(-1px);
}

button:focus {
    outline: 2px solid var(--color-secondary);
    outline-offset: 3px;
}


.video-background {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    overflow: hidden;
    z-index: -1;

}

video {
    width: 100%;
    height: 100%;
    object-fit: cover;
}

.overlay {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.5);
    /* Adjust opacity */
    z-index: 2;
}


@media (min-width: 1024px) {
    .content {
        width: 45%;
    }

    .container-flex {
        flex-direction: row;
        align-items: center;
        justify-content: space-between;
        gap: 3rem;
    }

    .content-flex {
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        gap: 0;

        div {
            text-align: center;
        }
    }

    .wrapper {
        width: 80%;
        height: 100%;
        margin: 0 auto;
        flex-direction: column;
        align-items: start;
        justify-content: space-evenly;
    }
}
</style>