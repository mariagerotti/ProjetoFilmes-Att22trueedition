<script>
import PictureCard from "../components/PictureCard.vue";
import FilmeApi from "../api/filme.js";
const filmeapi = new FilmeApi();
export default {
  components: { PictureCard },
  data() {
    return {
      filmes: [],
    };
  },
  async created() {
    this.filmes = await filmeapi.BuscaTodosOsFilmes();
  },
  methods: {
    getPosterUrl(posterPath) {
      return `https://image.tmdb.org/t/p/w500${posterPath}`;
    },
  },
};
</script>

<template>
  <div class="main">
    
    <div class="container">
      <PictureCard
        v-for="filme of filmes"
        :key="filme.id"
        :picture_src="getPosterUrl(filme.poster_path)"
        :pic_link="filme"
      />
    </div>
  </div>
</template>


<style>
body {
  width: 100%;
  place-items: center;
}
PictureCard {
  box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2);
  transition: 0.3s;
  width: 40%;
}

PictureCard:hover {
  box-shadow: 0 8px 16px 0 rgba(0,0,0,0.2);
}

.container {
  margin-top: 10%;
  max-height: 350px;
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 15px;
  flex-direction: row;
  flex-wrap: wrap;
}
.container:hover img {
  opacity: 0.3;
}
.container img:hover {
  opacity: 1;
}

#app {
  width: 100%;
  height: 100vh;
  display: grid;
  align-items: center;
  justify-items: stretch;
  align-content: stretch;
}
.titulo{
  font-family: sans-serif;
  margin-left: 10px;
  color: black;
}
</style>
