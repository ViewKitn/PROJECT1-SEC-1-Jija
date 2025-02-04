<script setup>
import { ref, watch } from "vue";
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

//feature trackRoundToScorePage
watch(round, () => {
  if (round.value >= 16) page.value = "score";
});

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
  }
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
      return "hover:bg-purple-500";
    case 1:
      return "hover:bg-blue-500";
    case 2:
      return "hover:bg-green-500";
    case 3:
      return "hover:bg-yellow-400";
    case 4:
      return "hover:bg-orange-500";
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
  checkAnswer(index);
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

const showtext = () => {
  if (score.value === 15) {
    return "Excellent!!!";
  } else if (score.value >= 12) {
    return "Perfect!!";
  } else if (score.value >= 9) {
    return "Great job!";
  } else if (score.value >= 5) {
    return "Good";
  } else {
    return "Not bad";
  }
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
          class="outline solid-1-black btn justify-center text-center [transition:_all_.3s_ease] disabled:bg-green-500 disabled:text-white no-underline leading-tight btn-outline-black bg-white text-pink hover:bg-emerald-500 hover:text-white hover:ring-white hover:ring-3 transition-all w-auto rounded-lg px-4 md:px-8 h-14 text-black font-bold mb-6 drop-shadow-lg uppercase hover:cursor-pointer"
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
        <h1 class="text-xl font-bold text-orange-500 shadow-lg mb-8">
          Category
        </h1>

        <div id="category-content" class="mt-8 grid grid-cols-2 gap-4 w-full">
          <div id="animals-content" class="category-item p-4">
            <h3 class="text-xl font-bold text-gray-800 mb-4">Animals</h3>
            <img
              src="./assets/imgs/category/animal.jpg"
              alt="Animals"
              class="w-full h-100 object-cover rounded-4xl mb-4"
            />
          </div>

          <div id="foods-content" class="category-item p-4">
            <h3 class="text-xl font-bold text-gray-800 mb-4">Fruits</h3>
            <img
              src="./assets/imgs/category/fruit.png"
              alt="Fruits"
              class="w-full h-100 object-cover rounded-4xl mb-4"
            />
          </div>

          <div id="objects-content" class="category-item p-4">
            <h3 class="text-xl font-bold text-gray-800 mb-4">Objects</h3>
            <img
              src="./assets/imgs/category/object.jpg"
              alt="Objects"
              class="w-full h-100 object-cover rounded-4xl mb-4"
            />
          </div>

          <div id="places-content" class="category-item p-4">
            <h3 class="text-xl font-bold text-gray-800 mb-4">Places</h3>
            <img
              src="./assets/imgs/category/wat.jpg"
              alt="Places"
              class="w-full h-100 object-cover rounded-4xl mb-4"
            />
          </div>
        </div>
      </div>
    </section>
    <!-- play game page -->
    <section v-show="page === 'play'" class="playgame-page">
      <!-- code here -->
      <div
        class="playgame-container w-full h-screen bg-linear-to-r from-purple-300 to-pink-600"
      >
        <!-- show-modal -->
        <div
          v-show="true"
          class="show-modal w-full h-screen flex z-10 bg-black/50"
        >
          <div class="modal-content w-0 h-[30%] self-center bg-white/90 ] ">
            <h1 class="w-fit mx-auto text-8xl text-green-600">Correct</h1>
            <p class="w-fit mx-auto my-4 text-2xl text-black">
              Answer: <span class="text-red-500">{{ answer }}</span>
            </p>
            <div class="btn-next flex justify-center">
              <button
                class="w-40 my-3 py-2 rounded-4xl text-2xl text-black bg-yellow-300 duration-200 ease-in hover:cursor-pointer hover:font-medium"
              >
                Next
              </button>
            </div>
          </div>
        </div>
        <!-- content-game -->
        <div class="game-content">
          <header class="flex">
            <div class="btn-back flex-1 self">
              <button
                @click="page = 'category'"
                class="w-40 mx-6 my-3 py-3 bg- rounded-4xl text-2xl text-black bg-zinc-100/70 duration-200 ease-in hover:cursor-pointer hover:bg-red-500 hover:text-white hover:font-medium"
              >
                Back
              </button>
            </div>

            <label class="swap flex-1">
              <!-- this hidden checkbox controls the state -->
              <input type="checkbox" />

              <!-- volume on icon -->
              <svg
                class="swap-on fill-current"
                xmlns="http://www.w3.org/2000/svg"
                width="48"
                height="48"
                viewBox="0 0 24 24"
              >
                <path
                  d="M14,3.23V5.29C16.89,6.15 19,8.83 19,12C19,15.17 16.89,17.84 14,18.7V20.77C18,19.86 21,16.28 21,12C21,7.72 18,4.14 14,3.23M16.5,12C16.5,10.23 15.5,8.71 14,7.97V16C15.5,15.29 16.5,13.76 16.5,12M3,9V15H7L12,20V4L7,9H3Z"
                />
              </svg>

              <!-- volume off icon -->
              <svg
                class="swap-off fill-current"
                xmlns="http://www.w3.org/2000/svg"
                width="48"
                height="48"
                viewBox="0 0 24 24"
              >
                <path
                  d="M3,9H7L12,4V20L7,15H3V9M16.59,12L14,9.41L15.41,8L18,10.59L20.59,8L22,9.41L19.41,12L22,14.59L20.59,16L18,13.41L15.41,16L14,14.59L16.59,12Z"
                />
              </svg>
            </label>
            <div class="round flex-1 self-center">
              <h1
                class="h-full mx-7 text-4xl text-end drop-shadow-lg font-bold"
              >
                {{ round }} / 15
              </h1>
            </div>
          </header>
          <div class="img-answer my-5">
            <img
              :src="`../imgs/animals/${answer}.jpg`"
              :alt="`img-${answer}`"
              class="w-lg h-80 mx-auto object-cover border-[1px] hover:scale-110 duration-150 hover:cursor-zoom-in"
            />
          </div>
          <h1 class="question my-14 text-7xl text-center font-medium">
            What is animal ?
          </h1>
          <div class="choice-list flex justify-around mt-24">
            <button
              v-for="(choice, index) in choiceList"
              :key="index"
              @click="nextRound('animal', index)"
              class="w-56 h-full mx-5 py-4 rounded-4xl bg-zinc-100/70 text-4xl text-black duration-200 ease-in hover:scale-125 hover:text-white hover:cursor-pointer hover:font-medium"
              :class="getColorButton(index)"
            >
              {{ choice }}
            </button>
          </div>
        </div>
      </div>
    </section>

    <!-- score page -->
    <section
      class="score-page h-screen bg-linear-to-r from-blue-500 to-pink-500 flex justify-center items-center"
      v-show="page === 'score'"
    >
      <div class="score-container text-4xl text-center">
        <h1 class="text-white text-9xl">{{ showtext() }}</h1>
        <h1
          class="py-16 text-blue-700 font-bold [font-family:'Lucida_Console',monospace]"
        >
          YOUR SCORE
        </h1>
        <div class="show-user-score my">
          <span class="rounded-3xl px-50 py-8 bg-gray-100 text-black"
            >{{ score }} / 15</span
          >
        </div>
        <div class="py-40 flex justify-center gap-30">
          <button
            @click="clearGame(), (page = 'home')"
            class="outline solid-1-black btn justify-center text-center [transition:_all_.3s_ease] text-black disabled:bg-[#B4BBC3A6] disabled:text-white no-underline leading-tight btn-outline-black bg-white text-pink hover:bg-[#0158C9] hover:text-white hover:ring-white hover:ring-2 transition-all w-auto rounded-lg px-4 md:px-8 h-14"
          >
            HOME
          </button>
          <button
            @click="clearGame(), gameStart('animal'), (page = 'play')"
            class="outline solid-1-black btn justify-center text-center [transition:_all_.3s_ease] text-black disabled:bg-[#B4BBC3A6] disabled:text-white no-underline leading-tight btn-outline-black bg-white text-pink hover:bg-[#0158C9] hover:text-white hover:ring-white hover:ring-2 transition-all w-auto rounded-lg px-4 md:px-8 h-14"
          >
            PLAY AGAIN
          </button>
          <video
            autoplay
            muted
            loop
            class="background-video absolute inset-0 w-full h-full object-cover mix-blend-screen"
          >
            <source src="./assets/video/Sequence01.webm" type="video/webm" />
          </video>
        </div>
      </div>
    </section>
  </div>
</template>

<style scoped>
.background-video {
  pointer-events: none;
}
.modal-content {
  animation-name: showmodal-animate;
  animation-duration: 1.5s;
  animation-timing-function: ease-in;
  animation-fill-mode: both;
}
@keyframes showmodal-animate {
  from{
    width: 0;
  } to {
    width: 100%;
  }
 
}
</style>
