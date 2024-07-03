<script setup>
import { reactive, ref, computed } from "vue";
import { items } from "./movies.json";
import movie from "./components/movie-component.vue";
import FormPopup from "./components/pop-up-component.vue";

const movies = reactive([...items]);
const show = ref(false);

const compmovies = computed(() => {
  return movies;
});

const infos = ref({
  id: undefined,
  name: "",
  description: "",
  image: "",
  inTheaters: [],
  genres: [],
});

const resetRatings = () => {
  movies.forEach((c, i) => {
    movies[i] = {
      ...movies[i],
      rating: 0,
    };
  });
};

const changeRating = ({ id, index }) => {
  const movieIndex = movies.findIndex((c) => c.id === id);

  if (movieIndex !== -1) {
    // atualização de filme já existente
    movies[movieIndex] = {
      ...movies[movieIndex],
      rating: index,
    };
  }
};

const excludeMovie = (id) => {
  const index = movies.findIndex((c) => c.id === id);
  if (index !== -1) {
    movies.splice(index, 1);
  }
};

const saveMovie = (infosparam) => {
  const movieIndex = movies.findIndex((c) => c.id === infosparam.id);

  if (movieIndex !== -1) {
    // atualização de filme já existente
    movies[movieIndex] = {
      ...movies[movieIndex],
      name: infosparam.name,
      description: infosparam.description,
      image: infosparam.image,
      inTheaters: !!infosparam.inTheaters,
      genres: infosparam.genres,
    };
  } else {
    // criação de novo filme
    const newId = Math.max(...movies.map((a) => a.id)) + 1;
    movies.push({
      id: newId,
      name: infosparam.name,
      description: infosparam.description,
      image: infosparam.image,
      inTheaters: !!infosparam.inTheaters,
      genres: infosparam.genres,
      rating: 0,
    });
  }
  dismissForm();
};

const editMovie = (id) => {
  const movieToEdit = movies.find((c) => c.id == id);
  if (movieToEdit) {
    infos.value = { ...movieToEdit };
    show.value = true;
  }
};

const dismissForm = () => {
  show.value = false;
  infos.value = {
    id: undefined,
    name: "",
    description: "",
    image: "",
    inTheaters: [],
    genres: [],
  };
};
</script>

<template>
  <div class="container-main">
    <div class="container-child">
      <div class="container-header-left">
        <h1 class="main-title"><span>Movies</span> and Series</h1>
        <h2>
          Total de Filmes: {{ movies.length }}    |    Média de avaliação:
          {{
            (
              movies.map((c) => c.rating).reduce((a, b) => a + b) / movies.length
            ).toFixed(1)
          }}
        </h2>
      </div>
      <div class="buttons">
        <button @click="resetRatings" class="btn">
          Remover avaliações
        </button>
        <button @click="show = true" class="btn">
          Adicionar novo filme
        </button>
      </div>
    </div>

    <div class="container-movies">
      <movie v-for="mov in compmovies" :key="mov.id" :image="mov.image" :title="mov.name" :description="mov.description"
        :rating="mov.rating" :tags="mov.genres" :id="mov.id" @exclude="excludeMovie" @edit="editMovie"
        @changeRating="changeRating" />
    </div>

    <FormPopup v-show="show" @submit="saveMovie" @dimiss="dismissForm" :infosprop="infos"></FormPopup>
  </div>
</template>

<style>
.container-main {
  display: flex;
  flex-direction: column;
  padding: 50px 100px;
}

.container-child {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
  width: 100%;
  margin-bottom: 40px;
}

.container-child h1 {
  color: #000;
}

.container-child h2 {
  font-size: 12px;
  margin-top: -2px;
}

.container-child h1.main-title {
  font-weight: 500;
  font-size: 40px;
}

.container-child h1 span {
  color: #E75A7C;
}

.container-movies {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-template-rows: 1fr;
  gap: 1rem;
  padding: 2.5rem;
  padding-top: 1.25rem;
}

.btn {
  padding: 10px 32px;
  background-color: #E75A7C;
  border: none;
  color: #fff;
  font-weight: 500;
  border-radius: 10px;
  font-size: 14px;
}

.buttons {
  display: flex;
  gap: 10px;
}
</style>