<script setup>
import { StarIcon, TrashIcon, PencilIcon } from "@heroicons/vue/24/solid";
import StarButton from "./star-component.vue";

defineProps([
  "image",
  "title",
  "description",
  "rating",
  "tags",
  "id"]);

const emit = defineEmits([
  "exclude",
  "edit",
  "changeRating"
]);
</script>

<template>
  <div class="container-main-movie">

    <!-- avaliação principal -->
    <div class="star-big">
      <div class="relative">
        <StarIcon class="star-icon" :class="{
          'text-yellow-500': rating != 0,
          'text-gray-500': rating == 0,
        }"></StarIcon>
        <h1 class="star-value" :class="{
          'text-yellow-800': rating != 0,
          'text-gray-300': rating == 0,
        }">
          {{ rating != 0 ? rating : "-" }}
        </h1>
      </div>
    </div>

    <!-- imagem da capa do filme/serie referente -->
    <img :src="image" class="h-[470px] object-cover w-full object-top" />

    <!-- informações sobre o filme/serie referente -->
    <div class="container-description">
      <div>
        <h1>{{ title }}</h1>
        <div class="flex space-x-1">
          <h2 v-for="tag in tags" class="flag" :key="tag">{{ tag }}</h2>
        </div>
        <p class="line-clamp-3">{{ description }}</p>
      </div>
      <div>
        <div class="text-value">Avaliação: ({{ rating }}/5)</div>
        <div class="star-container">
          <StarButton v-for="index in 5" :key="index" @starClicked="$emit('changeRating', { id, index })" :index="index"
            :currentRating="rating" />
        </div>
        <div class="interact-btns">
          <button @click="$emit('exclude', id)" class="button-2">
            <TrashIcon class="w-4 text-[#E75A7C]" />
          </button>
          <button @click="$emit('edit', id)" class="button-1">
            <PencilIcon class="w-4 text-gray-50" />
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.line-clamp-3 {
  display: -webkit-box;
  -webkit-box-orient: vertical;
  overflow: hidden;
}

.container-main-movie {
  width: 100%;
  border-radius: 10px;
  overflow: hidden;
  position: relative;
  border: 1px solid #bcbcbc
}

.star-big {
  position: absolute;
  right: 0;
}

.star-icon {
  width: 4rem;
  color: #f6e05e;
}

.star-value {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  font-weight: 600;
}

.container-description {
  background-color: #fff;
  padding: 15px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  height: 220px;
}

.container-description h1 {
  font-size: 20px;
  font-weight: 600;
}

.container-description p {
  font-size: 14px;
  margin-top: 10px;
  margin-bottom: 10px;
}

.flag {
  background-color: #E75A7C;
  color: #fff;
  display: inline-block;
  padding: 0.15rem 0.8rem;
  border-radius: 9999px;
  font-size: 0.75rem;
  font-weight: 500;
  margin-top: 10px;
}

span {
  display: flex;
  flex-direction: row;
}

.rating {
  font-size: 12px;
}

.interact-btns {
  position: absolute;
  display: flex;
  flex-direction: row;
  gap: 4px;
  right: 15px;
  bottom: 15px;
}

.interact-btns .button-1 {
  height: 35px;
  width: 35px;
  background-color: #E75A7C;
  border: 2px solid #E75A7C;
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: center;
  border-radius: 50%;
}

.interact-btns .button-2 {
  height: 35px;
  width: 35px;
  background-color: #ffffff;
  border: 2px solid #E75A7C;
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: center;
  border-radius: 50%;
}

.rating-text {
  display: block;
  margin-bottom: 8px;
}

.star-buttons {
  display: block;
}

.star-container {
  display: flex;
  gap: 2px;
  margin-bottom: 2px;
}

.text-value {
  font-size: 12px;
  margin-bottom: 2px;
}
</style>