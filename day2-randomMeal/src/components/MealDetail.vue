<script setup lang="ts">
import { ref, onMounted, reactive } from 'vue'

const meal = ref(null);
const ingredients = reactive([]);

onMounted(()=>{
    fetchMeal();
})

function fetchMeal() {
    fetch('https://www.themealdb.com/api/json/v1/1/random.php')
    .then(res => res.json())
    .then(json => {
        meal.value = json.meals[0];
        createMeal(json.meals[0]);
    })
    .catch(err => {
        console.warn(err);
    })
}

function createMeal(json) {
    const ingredientsArr = [];
    
    for(let i=1; i <= 20; i++) {
        if(json[`strIngredient${i}`]) {
            ingredientsArr.push(`${json[`strIngredient${i}`]} - ${json[`strMeasure${i}`]}`);
        } else {
            break;
        }
    }
    
    ingredients.value = ingredientsArr;
}

</script>

<template>
    <button id="getMealBtn" @click="fetchMeal">get meal</button>
    <div id="mealContent" v-if="meal">
        <div>
            <img :src="meal.strMealThumb" />
            <div><strong>Category:</strong> {{meal.strCategory}}</div>
            <div><strong>Area:</strong> {{meal.strArea}} </div>
            <div><strong>Ingredients:</strong></div>
            <ul v-for="ingredient in ingredients.value" v-if="ingredients.value">
                <li>{{ingredient}}</li>
            </ul>
        </div>
        <div>
            <h3>{{meal.strMeal}}</h3>
            <div>{{meal.strInstructions}}</div>
        </div>
    </div>
    <h3>Video Recipe</h3>
    <iframe width="1200" height="600" v-if="meal" :src="`https://www.youtube.com/embed/${meal.strYoutube.slice(-11)}`" />
</template>

<style scoped>
#mealContent {
    margin-top: 3rem;
    display: flex;
    width: 70vw;
    justify-content: center;
    gap: 2rem;
}

#mealContent img {
    width: 25rem;
}

#mealContent h3 {
    margin-top: 0;
}

#mealContent div:nth-child(1) {
    display: flex;
    flex-direction: column;
    gap:1rem;
}
#getMealBtn {
    width: 8rem;
    height: 2rem;
    text-transform: uppercase;
    border: 0;
    border-radius: 0.3rem;
    box-shadow: 3px 2px 2px rgba(0, 0, 0, 0.1);
    background-color: rgb(171, 81, 255);
    color: #fff;
    cursor: pointer;
    font-weight: 600;
    font-size: 0.8rem;
}

#getMealBtn:active, #getMealBtn:hover {
    background-color: blueviolet;
}

li {
    height: 0;
}

</style>