<template>
  <div class="container">
    <div class="flex flex-col items-center gap-y-4">
      <h1>Mes Recettes !!</h1>
      <input type="text" v-model="searchQuery" placeholder="Rechercher par titre..." class="border border-gray-300 rounded px-4 py-2 mt-4">
      <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-4">
        <div v-for="recipe in filteredRecipes" :key="recipe.id">
          <NuxtLink :to="'/recipes/' + recipe.id">
            <div class="bg-white rounded-lg shadow-md overflow-hidden cursor-pointer">
              <NuxtImg :src="recipe.img.url" class="w-full h-40 object-cover" alt="Recipe Image"></NuxtImg>
              <div class="p-4">
                <h2 class="text-xl font-semibold">{{ recipe.title }}</h2>
                <p class="mt-2 text-gray-600">{{ recipe.description }}</p>
              </div>
            </div>
          </NuxtLink>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'

const { find } = useStrapi()

const { data: recipes, pending, refresh, error } = await useAsyncData(
  'recipes',
  () => find('recipes', { populate: "*" })
)

const searchQuery = ref('')

const filteredRecipes = computed(() => {
  if (!searchQuery.value) {
    return recipes.data
  } else {
    return recipes.data.filter(recipe => recipe.title.toLowerCase().includes(searchQuery.value.toLowerCase()))
  }
})
</script>
