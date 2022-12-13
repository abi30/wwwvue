<template>

    <div class="flex gap-2 mt-2 justify-center">
        <router-link :to="{ name: 'byLetter', params: { letter } }" v-for="letter of letters" :key="letter">
            {{ letter }}
        </router-link>
    </div>
    <pre>
        <!-- {{ meals }} -->
    </pre>
    <div class="grid grid-cols-1 md:grid-cols-3 gap-5 p-8">
      <MealItem v-for="meal of meals" :key="meal.idMeal" :meal = "meal"></MealItem>
    </div>

</template>


<script setup>
import MealItem from '../components/MealItem.vue'
import { computed } from '@vue/reactivity';
import { onMounted , watch } from 'vue';
import { useRoute } from 'vue-router';
import store from '../store';

const route = useRoute();
const letters = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ'.split("");
const meals = computed(()=>store.state.mealsByLetter);

watch(route,()=>{
    store.dispatch("searchMealsByLetter",route.params.letter);  
})

onMounted(()=>{
    store.dispatch("searchMealsByLetter",route.params.letter);
});
</script>