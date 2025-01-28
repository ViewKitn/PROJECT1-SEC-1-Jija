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
  "avocado",
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
let score = ref(0);

const randomChoice = (arr) => {
  let count = 0;
  while (count < 5) {
    const index = Math.floor(Math.random() * arr.length);
    const randChoice = arr[index];
    if (
      !answerList.includes(randChoice) &&
      !choiceList.value.includes(randChoice)
    ) {
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

const addScore = () => {
  score.value += 1;
};
const resetScore = () => {
  score.value = 0;
};
const resetChoiceList = () => {
  choiceList.value.splice(0);
};
const resetAnswerList = () => {
  answerList.splice(0);
};
const checkAnswer = (index) => {
  if (answer.value === choiceList.value[index]) {
    addScore();
    console.log(score.value);
    return true;
  }
  return false;
};
const getColorButton = (index) => {
  switch (index) {
    case 0:
      return "hover:bg-red-500";
    case 1:
      return "hover:bg-blue-500 ";
    case 2:
      return "hover:bg-green-500";
    case 3:
      return "hover:bg-yellow-400";
    case 4:
      return "hover:bg-pink-400";
  }
};
const gameStart = (category) => {
  if (category === "animal") {
    randomChoice(animalList);
  } else if (category === "fruit") {
    randomChoice(fruitList);
  } else if (category === "country") {
    randomChoice(countryList);
  } else if (category === "equipment") {
    randomChoice(homeEquipmentList);
  }
  randomAnswer();
};

const nextRound = (category, index) => {
  console.log(checkAnswer(index));
  resetChoice();
  if (category === "animal") {
    randomChoice(animalList);
  } else if (category === "fruit") {
    randomChoice(fruitList);
  } else if (category === "country") {
    randomChoice(countryList);
  } else if (category === "equipment") {
    randomChoice(homeEquipmentList);
  }
  randomAnswer();
};

const clearGame = () => {
  resetScore();
  resetChoiceList();
  resetAnswerList();
  answer.value = "";
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
        <h1 class="answer text-4xl text-center">
          Answer: <span class="text-red-500">{{ answer }}</span>
        </h1>
        <div class="img-answer my-5">
          <img
            :src="`../imgs/animals/${answer}.jpg`"
            :alt="`img-${answer}`"
            class="w-lg h-80 object-cover mx-auto border-[1px]"
          />
        </div>
        <h1 class="question text-5xl text-center my-5">What is animal ?</h1>
        <div class="choice-list flex justify-around">
          <button
            v-for="(choice, index) in choiceList"
            :key="index"
            @click="nextRound('animal', index)"
            class="w-52 h-full my-3 mx-5 py-2 round
            ed-4xl bg-zinc-100 text-2xl duration-200 ease-in-out hover:scale-125 hover:text-white"
            :class="getColorButton(index)"
          >
            {{ choice }}
          </button>
        </div>
      </div>
    </section>
    <section class="score-page">
      <div class="score-contain text-4xl text-center my-20 bg-orange-200 h-100">
        <h1 class="py-16 text-blue-700 font-bold [font-family:'Lucida_Console',monospace]">YOUR SCORE</h1>
        <div class="show-user-score my">
          <span class="px-30 py-8 bg-gray-100">{{ score }}</span>
        </div>
        <div class="py-20 flex justify-center gap-30">
          <button @click="clearGame()" class="outline solid-1-black btn justify-center text-center [transition:_all_.3s_ease] disabled:bg-[#B4BBC3A6] disabled:text-white no-underline leading-tight btn-outline-black bg-white text-pink hover:bg-[#0158C9] hover:text-white hover:ring hover:ring-white hover:ring-2 transition-all w-auto rounded-lg px-4 md:px-8 h-14"> HOME </button>
          <button @click="gameStart()" class="outline solid-1-black btn justify-center text-center [transition:_all_.3s_ease] disabled:bg-[#B4BBC3A6] disabled:text-white no-underline leading-tight btn-outline-black bg-white text-pink hover:bg-[#0158C9] hover:text-white hover:ring hover:ring-white hover:ring-2 transition-all w-auto rounded-lg px-4 md:px-8 h-14"> PLAY AGAIN </button>
        </div>
      </div>
    </section>
  </div>
</template>

<style scoped></style>
