<template>
    <div class="container mx-auto p-4">
      <div v-if="recipe">
        <h1 class="text-2xl font-semibold">{{ recipe.title }}</h1>
        <div class="my-4">
          <NuxtImg :src="recipe.img.url" :alt="recipe.title" class="w-full h-auto"/>
        </div>
        <p class="text-gray-600">{{ recipe.description }}</p>
        <!-- Ajoutez d'autres détails de la recette ici -->
        <router-link to="/">Retour à la liste des recettes</router-link>
      </div>
      <div v-else>
        <p>Loading...</p>
      </div>
    </div>
  </template>
  
  <script setup>
  import { ref, onMounted } from 'vue'
  import { useStrapi } from '~/composables/strapi'
  
  const { find } = useStrapi()
  const recipe = ref(null)
  
  onMounted(async () => {
    const recipeId = $route.params.id
    recipe.value = await find('recipes', { id: recipeId })
  })
</script>  