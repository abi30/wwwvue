<template>
    <div class="p-8">
        <input 
        type="text"
        v-model = "keyword" 
        class="rounded border-2 border-gray-200 w-full" 
        placeholder="Search for Meals" 
        @change="searchMeals"/>
        search by name
    </div>
    <div class="grid grid-cols-1 md:grid-cols-3 gap-5 p-8">
       <div class="bg-white shadow rounded-xl" v-for="meal of meals" :key="meal.idMeal">
        <img class="rounded-t-xl w-full h-48 object-cover" :src="meal.strMealThumb" :alt="strMeal">
        <h3 class="p-3 font-semibold">{{ meal.strMeal }}</h3>
        <div class="p-3">
            <a :href="meal.strYoutube" target="_blank"> youtube </a>
            <router-link to="/">view</router-link>
        </div>
       </div>
    </div>
</template>


<script setup>
import {computed,ref} from 'vue';
import axiosClient from '../axiosClient';
import store from '../store';


const keyword = ref('');
const meals = computed(()=>store.state.searchedMeals);

function searchMeals(){

    store.dispatch('searchMeals',keyword.value);
   
}
</script>
