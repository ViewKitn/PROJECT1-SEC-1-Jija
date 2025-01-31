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
const answerList = [];
let answer = ref("");
let score = ref(0);
let round = ref(0);
let page = ref("home");

// feature score
const addScore = () => {
  score.value += 1;
};
const resetScore = () => {
  score.value = 0;
};

// feature round
const increaseRound = () => {
  round.value++;
};

const resetRound = () => {
  round.value = 0;
};

// feature choice
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

const resetChoiceList = () => {
  choiceList.value.splice(0);
};

// feature answer
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

const checkAnswer = (userSelect) => {
  if (answer.value === choiceList.value[userSelect]) {
    addScore();
    console.log(score.value);
    return true;
  }
  return false;
};

const resetAnswerList = () => {
  answerList.splice(0);
};

const resetAnswer = () => {
  answer.value = "";
};

// feature other
const getColorButton = (btnIndex) => {
  switch (btnIndex) {
    case 0:
      return "hover:bg-red-500";
    case 1:
      return "hover:bg-blue-500";
    case 2:
      return "hover:bg-green-500";
    case 3:
      return "hover:bg-yellow-400";
    case 4:
      return "hover:bg-pink-400";
  }
};

const gameStart = (category) => {
  increaseRound();
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
  increaseRound();
  console.log(checkAnswer(index));
  resetChoiceList();
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
  resetAnswer();
  resetRound();
};
</script>

<template>
  <div class="game-container">
    <!-- home page -->
    <section
      class="home-page h-screen flex flex-col place-items: center justify-center bg-linear-to-r from-fuchsia-400 to-blue-800"
      v-show="page === 'home'"
    >
      <!-- code here -->
      <div class="text-center">
        <h1 class="text-6xl font-bold mb-6 drop-shadow-lg text-white">
          Welcome to the Game!
        </h1>
        <p class="text-xl mb-8 opacity-90 text-white">
          What is it? Let's take a guess!😘
        </p>
        <button
          class="outline solid-1-black btn justify-center text-center [transition:_all_.3s_ease] disabled:bg-green-500 disabled:text-white no-underline leading-tight btn-outline-black bg-white text-pink hover:bg-emerald-500 hover:text-white hover:ring-white hover:ring-3 transition-all w-auto rounded-lg px-4 md:px-8 h-14 font-bold mb-6 drop-shadow-lg uppercase"
          @click="page = 'category'"
        >
          Play
        </button>
      </div>
    </section>

    <!-- category page -->
    <section class="category-page" v-show="page === 'category'">
      <!-- code here -->
      <button
        @click="gameStart('animal'), (page = 'play')"
        class="px-6 py-5 bg-green-400"
      >
        Start Game
      </button>
      <div
        id="app"
        class="flex flex-col items-center min-h-screen bg-gray-100 p-4"
      >
        <h1 class="text-5xl font-bold text-orange-500 shadow-lg mb-8">
          Category
        </h1>
        <div class="grid grid-cols-2 gap-4 w-full max-w-4xl">
          <div class="category-box p-4">
            <label class="flex items-center space-x-2 cursor-pointer">
              <input
                type="radio"
                v-model="selectedCategory"
                value="Animals"
                :disabled="isDisabled"
                class="form-radio text-orange-500"
              />
              <span class="text-lg">Animals</span>
            </label>
          </div>

          <div class="category-box p-4">
            <label class="flex items-center space-x-2 cursor-pointer">
              <input
                type="radio"
                v-model="selectedCategory"
                value="Foods"
                :disabled="isDisabled"
                class="form-radio text-orange-500"
              />
              <span class="text-lg">Foods</span>
            </label>
          </div>

          <div class="category-box p-4">
            <label class="flex items-center space-x-2 cursor-pointer">
              <input
                type="radio"
                v-model="selectedCategory"
                value="Objects"
                :disabled="isDisabled"
                class="form-radio text-orange-500"
              />
              <span class="text-lg">Objects</span>
            </label>
          </div>

          <div class="category-box p-4">
            <label class="flex items-center space-x-2 cursor-pointer">
              <input
                type="radio"
                v-model="selectedCategory"
                value="Places"
                :disabled="isDisabled"
                class="form-radio text-orange-500"
              />
              <span class="text-lg">Places</span>
            </label>
          </div>
        </div>

        <div v-if="selectedCategory === 'Animals'" class="mt-8">
          <h2 class="text-2xl font-bold text-gray-800">Category: Animals</h2>
          <!-- เว้นที่ใส่รูป -->
        </div>

        <div v-if="selectedCategory === 'Objects'" class="mt-8">
          <h2 class="text-2xl font-bold text-gray-800">Category: Objects</h2>
          <!-- รูป -->
        </div>

        <div v-if="selectedCategory === 'Foods'" class="mt-8">
          <h2 class="text-2xl font-bold text-gray-800">Category: Foods</h2>
          <!-- รูป -->
        </div>

        <div v-if="selectedCategory === 'Places'" class="mt-8">
          <h2 class="text-2xl font-bold text-gray-800">Category: Places</h2>
          <!-- รูป -->
        </div>
      </div>
    </section>

    <!-- play game page -->
    <section v-if="round <= 15" class="playgame-page" v-show="page === 'play'">
      <!-- code here -->
      <div class="playgame-container border-b-2">
        <header class="flex justify-between">
          <h1 class="mx-8 text-2xl">{{ round }} / 15</h1>
        </header>
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
            class="w-52 h-full my-3 mx-5 py-2 round ed-4xl bg-zinc-100 text-2xl duration-200 ease-in-out hover:scale-125 hover:text-white"
            :class="getColorButton(index)"
          >
            {{ choice }}
          </button>
        </div>
      </div>
    </section>

    <!-- score page -->
    <section class="score-page" v-show="page === 'score' || round === 16">
      <div class="score-container text-4xl text-center bg-orange-200 h-100">
        <h1
          class="py-16 text-blue-700 font-bold [font-family:'Lucida_Console',monospace]"
        >
          YOUR SCORE
        </h1>
        <div class="show-user-score my">
          <span class="px-30 py-8 bg-gray-100">{{ score }}/15</span>
        </div>
        <div class="py-20 flex justify-center gap-30">
          <button
            @click="clearGame(), (page = 'home')"
            class="outline solid-1-black btn justify-center text-center [transition:_all_.3s_ease] disabled:bg-[#B4BBC3A6] disabled:text-white no-underline leading-tight btn-outline-black bg-white text-pink hover:bg-[#0158C9] hover:text-white hover:ring-white hover:ring-2 transition-all w-auto rounded-lg px-4 md:px-8 h-14"
          >
            HOME
          </button>
          <button
            @click="clearGame(), gameStart('animal'), (page = 'play')"
            class="outline solid-1-black btn justify-center text-center [transition:_all_.3s_ease] disabled:bg-[#B4BBC3A6] disabled:text-white no-underline leading-tight btn-outline-black bg-white text-pink hover:bg-[#0158C9] hover:text-white hover:ring-white hover:ring-2 transition-all w-auto rounded-lg px-4 md:px-8 h-14"
          >
            PLAY AGAIN
          </button>
        </div>
      </div>
    </section>
  </div>
</template>

<style scoped></style>
