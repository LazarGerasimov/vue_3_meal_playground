
<template>
  <div class="p-8">
    <input v-model="keyword" type="text" class="w-full rounded border-2 border-gray-200" placeholder="Search for meals.."
      @change="searchMeals" />
  </div>

  <div class="grid grid-cols-1 md:grid-cols-3 gap-5 p-8">
    <div v-for="meal of meals" :key="meal.idMeal" class="bg-white shadow rounded-xl">
      <router-link :to="{ name: 'mealDetails', params: { id: meal.idMeal } }">
        <img :src="meal.strMealThumb" :alt="meal.strMeal" class="rounded-t-xl w-full h-56 object-cover" />
      </router-link>
      <div class="px-3">
        <h3 class="py-3 font-semibold text-center">{{ meal.strMeal }}</h3>
        <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Beatae non porro voluptatem alias delectus
          exercitationem nulla.
        </p>
        <div class=" py-2 flex items-center justify-between px-10">
          <a :href="meal.strYoutube" target="_blank"
            class="px-3 py-2 rounded border-2 border-red-500  bg-red-500 hover:bg-red-600 text-white transition-colors">
            Video
          </a>
          <router-link :to="{ name: 'mealDetails', params: { id: meal.idMeal } }"
            class="px-3 py-2 rounded border-2 border-blue-500  bg-blue-500 hover:bg-blue-600 text-white transition-colors">
            View
          </router-link>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>

import { ref, onMounted } from 'vue';
import store from '../store';
import { computed } from '@vue/reactivity';
import { useRoute } from 'vue-router';

const keyword = ref('');

const route = useRoute();

const meals = computed(() => store.state.searchedMeals);

function searchMeals() {
  store.dispatch('searchMeals', keyword.value)
};

onMounted(() => {
  keyword.value = route.params.name
  if (keyword.value) {
    searchMeals();
  }
})


</script>
