<script>
import axios from "axios";
import DescFilme from "../components/DescFilme.vue";
export default {
    components: {DescFilme},
    props: ["id"],
    data() {
        return {
            filme: {},
        };
    },
    async created() {
        const url = `https://api.themoviedb.org/3/movie/${this.id}?api_key=a37701b7a0845f3785cd83eb23add599&language=pt-BR`;
        const { data } = await axios.get(url);
        this.filme = data;
    },
  
};
</script>

<template>
  <div class="filmeback">
    {{ id }}
    <DescFilme :filme="filme" />
  </div>
</template>

<style>
.filmeback {
  background-color: #333;
}
main{
  margin-top: 10px;
}
.main p {
  display: flex;
  justify-content: center;
  font-size: 60px;
}

.descMovi {
  color: white;
  display: flex;
  justify-content: center;
  flex-direction: row-reverse;
  padding: 100px;
  margin-top: 1px;
  font-size: 30px;
}

.info-movi {
  display: flex;
  flex-direction: column;
  margin: 10px;
  margin-left: 5px;
}

.titulo {
  font-size: 75px;
}
.poster-filme-pag{
  width: 400px;
}
</style>