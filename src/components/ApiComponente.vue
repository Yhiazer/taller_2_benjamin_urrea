<template>
    <div>
        <h1>Opciones</h1>
        <div class="botones">
            <button @click="buscarPoblacion">Buscar Población</button>
            <button @click="buscarAnimeReco">Buscar Recomendaciones de Anime</button>
            <button @click="buscarAnimeR">Ver Anime Aleatorio</button>
            <button @click="buscarManga">Ver Manga Aleatorio</button>
        </div>
</div>
</template>

<script>

</script>

<style scoped>
button {
    margin: 10px;
    padding: 10px;
    width: 150px;
    background-color: #42b983;
    color: white;
    border: none;
    border-radius: 5px;
    cursor: pointer;
}

button:hover {
    background-color: #358a70;
}

.botones {
    display: flex;
    flex-direction: row;
}
</style>