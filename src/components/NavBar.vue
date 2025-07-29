<script setup lang="ts">

</script>

<template>
    <div class="nav-flex-column">
        <div>
            <img alt="Vue logo" class="logo" src="../../images/logo.png" width="64" height="64" />
        </div>
        <h2>🍔</h2>
    </div>

    <div class="nav-flex-row">
        <img alt="Vue logo" class="logo" src="../../images/logo.png" width="64" height="64" />
        <menu>
            <ul>
                <li><a href="#">Home</a></li>
                <li><a href="#">About</a></li>
                <li><a href="#">Contact</a></li>
                <li><a href="#">Services</a></li>
            </ul>
        </menu>
    </div>
</template>

<style scoped>
li {
    list-style: none;
}

ul {
    display: flex;
    flex-direction: row;
    gap: 20px;
    margin: 0;
    padding: 0;
}

a {
    text-decoration: none;
    color: var(--kopper-beige);
}

h1 {
    font-size: 1rem;
    font-weight: bold;
    margin: 0;
}

.nav-flex-column {
    width: 100%;
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: space-between;
    z-index: 1000;
}

.nav-flex-row {
    display: none;
    z-index: 1000;
}

@media (min-width: 1024px) {
    .nav-flex-row {
        width: 100%;
        display: flex;
        flex-direction: row;
        align-items: center;
        justify-content: center;
        gap: 10px;
    }

    .nav-flex-column {
        display: none;
    }
}
</style>