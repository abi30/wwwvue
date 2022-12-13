<template>
<div>
    <div class="flex flex-col p-8">
          
        <!-- <input type="text" class="rounded border-2 border-gray-200 w-full" placeholder="Search for Meals" /> -->


    
        <!-- <pre>{{ ingredients.meals }} </pre> -->
        
        <MealItem v-for="meal of ingredients.meals" :key="meal.idMeal" :meal = "meal"></MealItem>
       
    </div>
</div>
</template>

<script setup>
import MealItem from '../components/MealItem.vue'
import { computed,onMounted,ref } from 'vue';
import store from '../store';
import axiosClient from '../axiosClient.js';




const meals = computed(()=>store.state.searchedMeals);
const ingredients = ref([]);
onMounted(async() => {
  const response =   await axiosClient.get('list.php?i=list');
  console.log(response.data);
  ingredients.value = response.data;
    
});
</script>