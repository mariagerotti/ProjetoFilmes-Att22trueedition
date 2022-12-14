<script>
import { mapStores, mapState, mapActions } from "pinia";
import { useGenreStore } from "@/stores/genres";
export default {
  data() {
    return {
      genero: "",
    };
  },
  async created() {
    this.generos = await this.getAllGenres();
  },
  computed: {
    ...mapStores(useGenreStore),

    ...mapState(useGenreStore, ["genres"]),
  },
  methods: {
    ...mapActions(useGenreStore, ["getAllGenres"]),
    go() {
      this.$router.push(`/filmes_por_genero/${this.genero}`);
    },
    getProfileUrl(avatar_path) {
      return `https://image.tmdb.org/t/p/w500${avatar_path}`;
    },
  },
};
</script>

<template>
  <body>
    <header>
      <div class="content">
        <hgroup>
          <h1>
            <router-link class="routerlink" to="/" id="title">
              <h1><span>IM</span>ovies</h1>
            </router-link>
          </h1>
        </hgroup>
      </div>
      <div class="overlay"></div>
    </header>
    <section class="site">
      <nav>
        <router-link class="routerlink" to="/movie">Lançamentos</router-link>
        <select v-model="genero" @change="go" class="select-cabecalho">
          <option value="" disabled>Categorias</option>
          <option v-for="genero of genres" :key="genero.id" :value="genero.id">
            {{ genero.name }}
          </option>
        </select>
      </nav>
    </section>
  </body>
</template>

<style>
body {
  padding: 0;
  margin: 0;
  height: 100%;
  font-family: sans-serif;
}

header {
  height: 100%;
  position: relative;
  overflow: hidden;
  background: url(https://i.pinimg.com/564x/85/8b/e8/858be84f6a7fa8c70376b3f222a02b7d.jpg)
    center no-repeat;
  background-size: cover;
}

header .content {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  z-index: 1;
}

h1{
  color:rgb(73, 32, 112)
}

header h1,
header h2 {
  margin: 0;
}
select-cabecalho header h2 {
  text-transform: uppercase;
  margin-top: -0.5em;
}

header hgroup {
  -webkit-transform: translate(-50%, -50%);
  -moz-transform: translate(-50%, -50%);
  -ms-transform: translate(-50%, -50%);
  -o-transform: translate(-50%, -50%);
  transform: translate(-50%, -50%);
  display: inline-block;
  text-align: center;
  position: absolute;
  top: 50%;
  left: 50%;
  color: rgb(255, 255, 255);
  border: 5px solid #fff;
  padding: 0.5em 3em;
  font-size: 16px;
  text-decoration: none;
}

header .overlay {
  position: absolute;
  top: 0;
  right: 0;
  left: 0;
  bottom: 0;
  background: #333 center no-repeat;
  background-size: cover;
  z-index: 0;
  opacity: 0;
  -webkit-filter: blur(4px);
}

img {
  margin-right: 20px;
}

.site {
  padding: 10% 0;
  text-align: center;
  font-size: 0.8em;
  color: #444;
  position: relative;
}

.site a {
  color: #666;
  text-decoration: none;
}

.site a:hover {
  color: #222;
}

.site nav {
  position: absolute;
  top: 0;
  left: 0;
  background: #222;
  width: 100%;
}

.site nav a {
  padding: 10px 30px;
  font-size: 1.3em;
  display: inline-block;
  
}

.site nav a:hover {
  background: #333;
  color: #fff;
}
.select-cabecalho {
  appearance: none;
  background-color: #222;
  border: none;
  padding: 0 1em 0 0;
  margin: 0;
  width: 15%;
  cursor: inherit;
  line-height: inherit;
  font-size: inherit;
  color: #666;
}
option {
  margin: 0;
  text-align: center;
}
</style>
