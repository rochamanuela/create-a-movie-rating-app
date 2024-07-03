<script setup>
import { computed } from "vue";

const props = defineProps(["infosprop"]);
const infos = computed(() => {
  return props.infosprop;
});

const emit = defineEmits(["submit", "dimiss"]);
</script>

<template>
  <div class="container-main-form">
    <div class="container-form">
      <h1 class="title-modal">Nova obra</h1>
      <form v-on:submit.prevent="() => { $emit('submit', infos); }" class="container-form-content">
        <div class="container-form-content-child">
          <label for="name" class="label">Titulo</label>
          <input required name="name" v-model="infos.name" />

          <label for="description" class="label">Descrição</label>
          <textarea name="description" v-model="infos.description"></textarea>

          <label for="image" class="label">Imagem da capa</label>
          <input name="image" v-model="infos.image" />
        </div>
        <div class="container-form-content-child">
          <label for="genres" class="label">Gêneros</label>
          <select required multiple name="genres" v-model="infos.genres" class="custom-select">
            <option value="Fantasia">Fantasia</option>
            <option value="Romance">Romance</option>
            <option value="Comédia">Comédia</option>
            <option value="Ação">Ação</option>
            <option value="Aventura">Aventura</option>
            <option value="Drama">Drama</option>
            <option value="Crime">Crime</option>
            <option value="Terror">Terror</option>
          </select>

          <div>
            <label for="checkbox" class="cartaz">
              <input type="checkbox" name="checkbox" v-model="infos.inTeathers" />
              <p>Em cartaz nos cinemas</p>
            </label>
          </div>

          <div class="buttons-container">
            <button @click="$emit('dimiss')" type="button">cancelar</button>
            <button type="submit">salvar</button>
          </div>
        </div>
      </form>
    </div>
  </div>
</template>

<style>
.container-main-form {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  top: 0;
  backdrop-filter: blur(4px);
  background-color: rgba(0, 0, 0, 0.2);
  display: flex;
  align-items: center;
  justify-content: center;
}

.container-form {
  width: 50%;
  height: auto;
  padding: 30px;
  background-color: #ffffff;
  margin-top: 5rem;
  border-radius: 10px;
}

.container-form-content {
  display: flex;
  flex-direction: row;
  height: auto;
  justify-content: space-between;
  gap: 30px;
}

.container-form-content-child {
  display: flex;
  flex-direction: column;
  width: 100%;
}

input {
  background-color: #fff;
  color: #000;
  border-radius: 7px;
  outline: none;
  border: 2px solid #000;
  height: 44px;
  text-indent: 15px;
}

textarea {
  background-color: #fff;
  color: #000;
  border-radius: 7px;
  outline: none;
  border: 2px solid #000;
  height: 150px;
  text-indent: 15px;
  padding-top: 10px;
  resize: none;
}

.label {
  font-weight: 500;
  color: #000;
  margin-bottom: 5px;
  margin-top: 15px;
}

label.cartaz {
  display: flex;
  flex-direction: row;
  gap: 10px;
  align-items: center;
}

.title-modal {
  font-size: 30px;
  font-weight: 500;
}

.custom-select {
  appearance: none;
  -webkit-appearance: none;
  -moz-appearance: none;
  border: 2px solid #000000;
  border-radius: 5px;
  background-color: #fff;
  width: 100%;
  max-width: 100%;
  box-sizing: border-box;
  cursor: pointer;
  outline: none;
  transition: border-color 0.2s ease;
}

.custom-select option {
  padding: 8px 14px;
  font-size: 14px;
  background-color: #fff;
  color: #000;
}

.custom-select[multiple] {
  height: auto;
  min-height: 100px;
  overflow-y: auto;
}

.custom-select::-webkit-scrollbar {
  width: 8px;
}

.custom-select::-webkit-scrollbar-thumb {
  background-color: #ccc;
  border-radius: 4px;
}

.buttons-container {
  display: flex;
  gap: 5px;
  justify-content: flex-end;
  margin-top: 85px;
}

.buttons-container :first-child {
  background-color: #fff;
  color: #E75A7C;
  border: 2px solid #E75A7C;
}

.buttons-container :last-child {
  background-color: #E75A7C;
  border: 2px solid #E75A7C;
  color: #fff;
}

.buttons-container :first-child, .buttons-container :last-child {
  padding: 10px 20px;
  font-size: 14px;
  font-weight: 500;
  border-radius: 10px;
}
</style>