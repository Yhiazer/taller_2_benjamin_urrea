<template>
    <div>
        <h1>Opciones</h1>
        <div class="botones">
            <button @click="buscarPoblacion">Buscar Población</button>
            <button @click="buscarAnimeReco">Buscar Recomendaciones de Anime</button>
            <button @click="buscarAnimeR">Ver Anime Aleatorio</button>
            <button @click="buscarManga">Ver Manga Aleatorio</button>
        </div>

        <div v-if="data">
            <h2>Resultado:</h2>
            <div v-if="dataType === 'poblacion'">
                <ul>
                    <li v-for="pais in data" :key="pais.country">{{ pais.country }}: {{ pais.populationCounts[0].value }} habitantes</li>
                </ul>
            </div>
            <div v-else-if="dataType === 'animeReco'">
                <ul>
                    <li v-for="anime in data" :key="anime.entry.title">{{ anime.entry.title }} - Score: {{ anime.score }}</li>
                </ul>
            </div>
            <div v-else-if="dataType === 'randomAnime'">
                <p>{{ data.title }} ({{ data.genres.map(g => g.name).join(', ') }})</p>
            </div>
            <div v-else-if="dataType === 'randomManga'">
                <p>{{ data.title }} por {{ data.authors.map(a => a.name).join(', ') }}</p>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            data: null, 
            dataType: ''
        };
    },
    methods: {
        async buscarPoblacion() {
            try {
                const response = await fetch('https://countriesnow.space/api/v0.1/countries/population');
                const result = await response.json();
                this.data = result.data; 
                this.dataType = 'poblacion';
            } catch (error) {
                console.error("Error al obtener la población de países:", error);
            }
        },

        async buscarAnimeReco() {
            try {
                const response = await fetch('https://api.jikan.moe/v4/recommendations/anime');
                const result = await response.json();
                this.data = result.data;
                this.dataType = 'animeReco'; 
            } catch (error) {
                console.error("Error al obtener recomendaciones de anime:", error);
            }
        },

        async buscarAnimeR() {
            try {
                const response = await fetch('https://api.jikan.moe/v4/random/anime');
                const result = await response.json();
                this.data = result.data; 
                this.dataType = 'randomAnime'; 
            } catch (error) {
                console.error("Error al obtener anime aleatorio:", error);
            }
        },

        async buscarManga() {
            try {
                const response = await fetch('https://api.jikan.moe/v4/random/manga');
                const result = await response.json();
                this.data = result.data; 
                this.dataType = 'randomManga'; 
            } catch (error) {
                console.error("Error al obtener manga aleatorio:", error);
            }
        },
    },
};
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