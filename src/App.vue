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
  "philippine",
  "russia",
  "portugal",
];
const homeEquipmentList = [
  "refrigerator",
  "microwave",
  "dishwasher",
  "washing machine",
  "clothes iron",
  "hair dryer",
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

// variable
const choiceList = ref([]);
const answerList = [];
let answer = ref("");
let score = ref(0);
let round = ref(0);
let page = ref("home");
let category = ref("");
let time = ref(5);
let modal = ref("close");
let stateAnswer = ref("");
let setintervalTimerId;
let modalContent = ref("close");

//feature timer
const startTimer = () => {
  setintervalTimerId = setInterval(() => {
    time.value -= 1;
    if (time.value === 0) {
      stateAnswer.value = "incorrect";
      showmodal();
      stopTimer(setintervalTimerId);
    }
  }, 1000);
};
const stopTimer = (timerId) => {
  clearInterval(timerId);
  time.value = 5;
};

// feature score
const addScore = () => {
  score.value += 1;
};
const resetScore = () => {
  score.value = 0;
};

//feature trackRoundToScorePage
watch(round, () => {
  if (round.value >= 16) {
    page.value = "score";
    stopTimer(setintervalTimerId);
  }
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
    stateAnswer.value = "correct";
  } else {
    stateAnswer.value = "incorrect";
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

const gameStart = () => {
  startTimer();
  increaseRound();
  if (category.value === "animal") {
    randomChoice(animalList);
  } else if (category.value === "fruit") {
    randomChoice(fruitList);
  } else if (category.value === "country") {
    randomChoice(countryList);
  } else if (category.value === "equipment") {
    randomChoice(homeEquipmentList);
  }
  randomAnswer();
};

const nextRound = () => {
  increaseRound();
  resetChoiceList();
  startTimer();
  showmodal();
  if (category.value === "animal") {
    randomChoice(animalList);
  } else if (category.value === "fruit") {
    randomChoice(fruitList);
  } else if (category.value === "country") {
    randomChoice(countryList);
  } else if (category.value === "equipment") {
    randomChoice(homeEquipmentList);
  }
  randomAnswer();
};

const clearGame = () => {
  stopTimer(setintervalTimerId);
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

const showmodal = () => {
  if (modal.value !== "show") {
    modal.value = "show";
    setTimeout(() => (modalContent.value = "show"),300);
  } else {
    modal.value = "close";
    modalContent.value = "close"
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

      <div
        id="app"
        class="flex flex-col items-center min-h-screen bg-gray-100 p-4 bg-linear-to-r from-yellow-200 to-red-400"
      >
        <h1 class="text-4xl font-bold text-purple-800 shadow-lg mb-8">
          Category
        </h1>

        <div id="category-content" class="mt-8 grid grid-cols-2 gap-4 w-full">
          <div id="animals-content" class="category-item p-4">
            <h3 class="text-2xl font-bold text-gray-800 mb-4">Animals</h3>
            <img
              src="./assets/imgs/category/animal.jpg"
              alt="Animals"
              class="w-[95%] h-100 object-cover rounded-4xl mb-4 hover:scale-110"
              @click="(category = 'animal'), gameStart(), (page = 'play')"
            />
          </div>

          <div id="foods-content" class="category-item p-4">
            <h3 class="text-2xl font-bold text-gray-800 mb-4">Fruits</h3>
            <img
              src="./assets/imgs/category/fruit.png"
              alt="Fruits"
              class="w-[95%] h-100 object-cover rounded-4xl mb-4 hover:scale-110"
              @click="(category = 'fruit'), gameStart(), (page = 'play')"
            />
          </div>

          <div id="objects-content" class="category-item p-4">
            <h3 class="text-2xl font-bold text-gray-800 mb-4">Equipments</h3>
            <img
              src="./assets/imgs/category/equipment.jpg"
              alt="Objects"
              class="w-[95%] h-100 object-cover rounded-4xl mb-4 hover:scale-110"
              @click="(category = 'equipment'), gameStart(), (page = 'play')"
            />
          </div>

          <div id="places-content" class="category-item p-4">
            <h3 class="text-2xl font-bold text-gray-800 mb-4">Countries</h3>
            <img
              src="./assets/imgs/category/country.png"
              alt="Places"
              class="w-[95%] h-100 object-cover rounded-4xl mb-4 hover:scale-110"
              @click="(category = 'country'), gameStart(), (page = 'play')"
            />
          </div>
        </div>
      </div>
    </section>
    <!-- play game page -->
    <section v-show="page === 'play'" class="playgame-page">
      <!-- code here -->
      <div
        class="playgame-container w-full bg-linear-to-r from-purple-300 to-pink-600"
      >
        <!-- show-modal -->
        <div
          v-show="modal === 'show'"
          class="show-modal w-full h-screen flex justify-center fixed z-10 bg-black/50"
        >
          <div class="modal-slide w-0 h-[30%] self-center bg-white/90 ]">
            <div v-show="modalContent === 'show'" class="modal-content">
              <h1 class="w-fit mx-auto text-8xl text-green-600">
                {{ stateAnswer === "correct" ? "Correct" : "Incorrect" }}
              </h1>
              <p v-show="stateAnswer === 'correct'" class="w-fit mx-auto my-4  text-2xl text-black">Bravo</p>
              <p
                v-show="stateAnswer === 'incorrect'"
                class="w-fit mx-auto my-4 text-2xl text-black"
              >
                Answer: <span class="text-red-500">{{ answer }}</span>
              </p>
              <div class="btn-next flex justify-center">
                <button
                  @click="nextRound()"
                  class="w-40 my-3 py-2 rounded-4xl text-2xl text-black bg-yellow-300 duration-200 ease-in hover:cursor-pointer hover:font-medium"
                >
                  Next
                </button>
              </div>
            </div>
          </div>
        </div>
        <!-- content-game -->
        <div class="game-content w-full h-screen">
          <header class="flex h-24">
            <div class="btn-back flex-1 self-center">
              <button
                @click="clearGame(), (page = 'category')"
                class="w-40 mx-6 py-3 bg- rounded-4xl text-2xl text-black bg-zinc-100/70 duration-200 ease-in hover:cursor-pointer hover:bg-red-500 hover:text-white hover:font-medium"
              >
                Back
              </button>
            </div>
            <div class="timer self-center">
              <h1 class="text-4xl font-bold">{{ time }}</h1>
            </div>
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
              :src="`../imgs/${category}s/${answer}.jpg`"
              :alt="`img-${answer}`"
              class="w-lg h-80 mx-auto object-cover border-[1px] hover:scale-110 duration-150 hover:cursor-zoom-in"
            />
          </div>
          <h1 class="question my-14 text-7xl text-center font-medium">
            What is {{ category }} ?
          </h1>
          <div class="choice-list flex justify-around mt-24">
            <button
              v-for="(choice, index) in choiceList"
              :key="index"
              @click="
                stopTimer(setintervalTimerId), checkAnswer(index), showmodal()
              "
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
            @click="clearGame(), gameStart(), (page = 'play')"
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
.modal-slide {
  animation-name: showmodal-animate;
  animation-duration: 0.3s;
  animation-timing-function: ease-in;
  animation-fill-mode: both;
}
@keyframes showmodal-animate {
  from {
    width: 0;
  }
  to {
    width: 100%;
  }
}
</style>
