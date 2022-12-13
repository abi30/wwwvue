<template>
    <div class="p-8 pb-0">
        <input 
        type="text"
        v-model = "keyword" 
        class="rounded border-2 border-gray-200 w-full" 
        placeholder="Search for Meals" 
        @change="searchMeals"/>
    </div>
    <div class="grid grid-cols-1 md:grid-cols-3 gap-5 p-8">
        <div class="bg-white shadow rounded-xl" v-for="meal of meals" :key="meal.idMeal">
        <router-link :to="{name:'mealDetails',params:{id:meal.idMeal}}">
             <img class="rounded-t-xl w-full h-64 object-cover" :src="meal.strMealThumb" :alt="strMeal"/>
         </router-link>

        <div class="p-3">
            <h3 class="font-bold">{{ meal.strMeal }}</h3>
            <p class="mb-4">Lorem ipsum dolor sit, amet consectetur adipisicing elit. Commodi aliquid facere laudantium nemo corporis inventore culpa deserunt
                 saepe.officia adipisci assumenda?</p>
            <div class="flex items-center justify-between">
             
                <YoutubeButton :href="meal.strYoutube">Youtube</YoutubeButton>
                <!-- <router-link
                class="px-3 py-2 rounded border-2 text-white  border-purple-500 bg-purple-500 hover:bg-purple-600 hover:border-purple-600 hover:text-white transition-colors

                " 
                 to="/">view</router-link> -->
            </div>

        </div>
       </div>


    </div>
</template>


<script setup>
import {computed} from '@vue/reactivity';
import {onMounted,ref} from 'vue';
import axiosClient from '../axiosClient';
import { useRoute } from 'vue-router';
import store from '../store';
import YoutubeButton from '../components/YoutubeButton.vue';


const route = useRoute();
const keyword = ref('');
const meals = computed(()=>store.state.searchedMeals);

function searchMeals(){

    store.dispatch('searchMeals',keyword.value);
   
}

onMounted(() => {
    keyword.value = route.params.name
    if(keyword.value){
        searchMeals();
    }
})
</script>
