
<template>
  <div class="p-8">
    <input v-model="keyword" type="text" class="w-full rounded border-2 border-gray-200" placeholder="Search for meals.."
      @change="searchMeals" />
  </div>

  <div>
    <pre>{{ meals }}</pre>
  </div>
</template>

<script setup>

import { ref } from 'vue';
import store from '../store';
import { computed } from '@vue/reactivity';

const keyword = ref('');
const meals = computed(() => store.state.searchedMeals);

function searchMeals() {
  store.dispatch('searchMeals', keyword.value)
}

</script>
