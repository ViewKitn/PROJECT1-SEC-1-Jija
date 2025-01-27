<script setup>
import { ref } from "vue";
const animalList = [
  "monkey",
  "shark",
  "bear",
  "camel",
  "donkey",
  "rabbit",
  "zebra",
  "dog",
  "cat",
  "deer",
  "squirrel",
  "fox",
  "pig",
  "horse",
  "cheetah",
  "elephant",
  "giraffe",
  "cow",
  "goat",
  "butterfly",
];
const fruitList = [
  "apple",
  "banana",
  "blueberry",
  "cherry",
  "cantaloupe",
  "grape",
  "durian",
  "kiwi",
  "lemon",
  "lime",
  "mangosteen",
  "mango",
  "lychee",
  "orange",
  "pineapple",
  "rambutan",
  "starfruit",
  "strawberry",
  "watermelon",
  "papaya",
];
const countryList = [
  "argentina",
  "australia",
  "brazil",
  "cambodia",
  "china",
  "america",
  "egypt",
  "finland",
  "france",
  "georgia",
  "germany",
  "iceland",
  "india",
  "indonesia",
  "italy",
  "japan",
  "mexico",
  "philippines",
  "russia",
  "portugal",
];
const homeEquipmentList = [
  "refrigerator",
  "microwave",
  "dishwasher",
  "washing machine",
  "clothes iron",
  "hair dyer",
  "air conditioner",
  "heater",
  "electric fan",
  "coffee maker",
  "blender",
  "rice cooker",
  "oven",
  "television",
  "clock",
  "computer",
  "lamp",
  "speaker",
  "griddle",
  "toothbrush",
];
const choiceList = ref([]);
let answer = ref("");
const answerList = [];
const randomChoice = (arr) => {
  let count = 0;
  while (count < 5) {
    const index = Math.floor(Math.random() * arr.length);
    const randChoice = arr[index];
    if (!answerList.includes(randChoice) && !choiceList.value.includes(randChoice)) {
      choiceList.value.push(randChoice);
      count++;
    }
  }
};
const randomAnswer = () => {
  while (true) {
    const index = Math.floor(Math.random() * choiceList.value.length);
    answer.value = choiceList.value[index];
    if (!answerList.includes(answer.value)) {
      answerList.push(answer.value);
      break;
    }
  }
};

const nextRound = (category) => {
  choiceList.value.splice(0);
  if (category === "animal") {
    randomChoice(animalList);
  } else if (category === "fruit") {
    randomChoice(fruitListList);
  } else if (category === "country") {
    randomChoice(countryListList);
  } else if (category === "equipment") {
    randomChoice(homeEquipmenList);
  }
  randomAnswer();
};

</script>

<template>
  <div class="game-container">
    <section class="home-page">
      <!-- code here -->
    </section>
    <section class="category-page">
      <!-- code here -->
    </section>
    <section class="playgame-page">
      <!-- code here -->
      <div class="playgame-container">
        <button @click="gameStart('animal')" class="px-6 py-5 bg-green-400">
          Start Game
        </button>
        <h1 class="answer text-4xl">
          Answer: <span class="text-red-500">{{ answer }}</span>
        </h1>
        <div class="choice-list">
          <button
            v-for="(choice, index) in choiceList"
            :key="index"
            @click="nextRound('animal')"
            class="my-3 mx-5 py-3 px-5 bg-orange-400 text-2xl"
          >
            {{ choice }}
          </button>
        </div>
      </div>
    </section>
    <section class="score-page">
      <!-- code here -->
    </section>
  </div>
</template>

<style scoped></style>
