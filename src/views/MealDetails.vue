<template>
  <div class="w-[800px] mx-auto">

    <h1 class="text-5xl font-bold mb-5 text-center mt-5">{{ meal.strMeal }}</h1>
    <img :src="meal.strMealThumb" alt="meal.strMeal" class="w-[550px] mx-auto rounded-xl">

    <div class=" py-2 flex items-center justify-center px-10 mt-5">
      <a :href="meal.strYoutube" target="_blank"
        class="px-3 py-2 rounded border-2 border-red-500  bg-red-500 hover:bg-red-600 text-white transition-colors">
        Video guide
      </a>
    </div>


    <div class="grid grid-cols-1 md:grid-cols-3 text-lg py-2 mx-auto mt-10">
      <div>
        <strong class="font-bold">Category:</strong> {{ meal.strCategory }}
      </div>
      <div>
        <strong class="font-bold">Category:</strong> {{ meal.strArea }}
      </div>
      <div>
        <strong class="font-bold">Tags:</strong> {{ meal.strTags }}
      </div>
    </div>



    <div class="grid grid-cols-1 md:grid-cols-2 mt-10">
      <div>
        <h2 class="text-2xl font-semibold mb-2 text-center">Ingredients</h2>
        <!-- output all ingredients -->
        <ul class="text-center">
          <template v-for="(element, index) of new Array(20)">
            <li v-if="meal[`strIngredient${index + 1}`]">
              {{ index + 1 }}. {{ meal[`strIngredient${index + 1}`] }}
            </li>
          </template>
        </ul>
      </div>
      <div>
        <h2 class="text-2xl font-semibold mb-3 text-center">Measures</h2>
        <!-- output all ingredients -->
        <ul class="text-center">
          <template v-for="(element, index) of new Array(20)">
            <li v-if="meal[`strMeasure${index + 1}`]" class="ml-4">
              - {{ meal[`strMeasure${index + 1}`] }}
            </li>
          </template>
        </ul>
      </div>
    </div>

  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import { useRoute } from 'vue-router'
import axiosClient from '../axiosClient';

const route = useRoute();
const meal = ref();

onMounted(() => {
  axiosClient.get(`lookup.php?i=${route.params.id}`)
    .then(({ data }) => {
      meal.value = data.meals[0] || {};
    })
})

</script>