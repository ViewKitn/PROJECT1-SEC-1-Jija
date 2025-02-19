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
const complimentList = ["Bravo", "Nice", "Great", "Awesome", "Fabulous"];

// variable
const choiceList = ref([]);
const answerList = [];
let stateAnswer = ref("");
let answer = ref("");
let score = ref(0);
let round = ref(0);
let page = ref("home");
let category = ref("");
let modal = ref("close");
let modalContent = ref("close");
let time = ref(5);
let setintervalTimerId;
const musicPlayer = ref("starting");
const onMusic = ref(false);
let complimentText = ref("");

// feature audio
const playMusic = () => {
  onMusic.value = !onMusic.value;
  if (onMusic.value) musicPlayer.value.play();
  else musicPlayer.value.pause();
};
const playClickSound = () => {
  const audio = new Audio("/audios/OnClick-1.wav");
  audio.play();
};
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

const showCompliment = () => {
  const randomCompliment =
    complimentList[Math.floor(Math.random() * complimentList.length)];
  complimentText.value = randomCompliment;
  return randomCompliment;
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

const checkAnswer = (userSelect) => {
  if (answer.value === choiceList.value[userSelect]) {
    addScore();
    stateAnswer.value = "correct";
    showCompliment();
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
      return "hover:bg-pink-400";
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
    return "Excellent🏆";
  } else if (score.value >= 12) {
    return "Perfect🏅";
  } else if (score.value >= 9) {
    return "Great job!⭐";
  } else if (score.value >= 5) {
    return "Good👍";
  } else {
    return "Not bad✨";
  }
};

const showmodal = () => {
  if (modal.value !== "show") {
    modal.value = "show";
    setTimeout(() => (modalContent.value = "show"), 300);
  } else {
    modal.value = "close";
    modalContent.value = "close";
  }
};
</script>

<template>
  <div class="game-container">
    <section
      class="home-page h-screen flex flex-col place-items: center justify-center bg-linear-to-r from-fuchsia-600 to-blue-800"
      v-show="page === 'home'"
    >
      <video
        autoplay
        muted
        loop
        class="background-video-first absolute inset-0 w-full h-full object-cover mix-blend-screen opacity-30"
      >
        <source src="./assets/video/Sequence1.webm" type="video/webm" />
      </video>

      <div class="btn-audio absolute top-4 right-7">
        <label class="swap bg-red-600 h-25 w-25 rounded-full">
          <input type="checkbox" @click="playMusic" v-model="onMusic" />
          <svg
            class="swap-on fill-current"
            xmlns="http://www.w3.org/2000/svg"
            width="70"
            height="70"
            viewBox="0 0 24 24"
            style="color: white"
          >
            <path
              d="M14,3.23V5.29C16.89,6.15 19,8.83 19,12C19,15.17 16.89,17.84 14,18.7V20.77C18,19.86 21,16.28 
              21,12C21,7.72 18,4.14 14,3.23M16.5,12C16.5,10.23 15.5,8.71 14,7.97V16C15.5,15.29 16.5,13.76 16.5,12M3,9V15H7L12,20V4L7,9H3Z"
            />
          </svg>

          <svg
            class="swap-off fill-current"
            xmlns="http://www.w3.org/2000/svg"
            width="70"
            height="70"
            viewBox="0 0 24 24"
            style="color: white"
          >
            <path
              d="M3,9H7L12,4V20L7,15H3V9M16.59,12L14,9.41L15.41,8L18,10.59L20.59,8L22,9.41L19.41,12L22,
              14.59L20.59,16L18,13.41L15.41,16L14,14.59L16.59,12Z"
            />
          </svg>
        </label>
        <audio controls class="hidden" ref="musicPlayer" loop>
          <source src="/audios/GameMusic.mp3" type="audio/mp3" />
          <p>
            Your browser doesn't support this audio file. Here is a
            <a href="/audios/GameMusic.mp3">link to the audio</a>
            instead.
          </p>
        </audio>
      </div>
      <div class="text-center bg-black rounded-lg h-130">
        <h1 class="text-8xl font-bold pt-21 mb-6 drop-shadow-lg text-white">
          Welcome to the Game!
        </h1>
        <p class="text-3xl mb-10 opacity-90 text-white">
          What is it? Let's take a guess !?😘
        </p>
        <button
          class="outline justify-center text-center [transition:_all_.3s_ease] leading-tight bg-white hover:bg-yellow-400 hover:text-white hover:ring-white hover:ring-3 transition-all w-auto rounded-full px-8 md:px-12 h-28 text-6xl text-purple-500 font-bold mb-6 drop-shadow-lg uppercase hover:cursor-pointer"
          @click="(page = 'category'), playClickSound()"
        >
          Play
        </button>
      </div>
    </section>

    <section class="category-page" v-show="page === 'category'">
      <div
        id="app"
        class="flex flex-col items-center min-h-screen p-4 bg-linear-to-r from-fuchsia-500 to-blue-600"
      >
        <h1 class="text-8xl font-bold text-white shadow-lg pt-15 mb-15">
          Category
        </h1>

        <div
          id="category-content"
          class="mt-8 grid grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-6 w-full"
        >
          <video
            autoplay
            muted
            loop
            class="background-video-second absolute inset-0 w-full h-full object-cover mix-blend-screen"
          >
            <source src="./assets/video/Sequence2.webm" type="video/webm" />
          </video>
          <div
            id="animals-content"
            class="category-item p-4 bg-yellow-300 rounded-lg"
          >
            <h3 class="text-4xl font-bold text-gray-800 mb-4">Animals</h3>
            <img
              src="./assets/imgs/category/animal.jpg"
              alt="Animals"
              class="w-[100%] h-100 object-cover rounded-4xl mb-4 hover:scale-110"
              @click="
                (category = 'animal'),
                  gameStart(),
                  (page = 'play'),
                  playClickSound()
              "
            />
          </div>

          <div
            id="foods-content"
            class="category-item p-4 bg-green-400 rounded-lg"
          >
            <h3 class="text-4xl font-bold text-gray-800 mb-4">Fruits</h3>
            <img
              src="./assets/imgs/category/fruit.png"
              alt="Fruits"
              class="w-[100%] h-100 object-cover rounded-4xl mb-4 hover:scale-110"
              @click="
                (category = 'fruit'),
                  gameStart(),
                  (page = 'play'),
                  playClickSound()
              "
            />
          </div>

          <div
            id="objects-content"
            class="category-item p-4 bg-blue-300 rounded-lg"
          >
            <h3 class="text-4xl font-bold text-gray-800 mb-4">Equipments</h3>
            <img
              src="./assets/imgs/category/equipment.jpg"
              alt="Objects"
              class="w-[100%] h-100 object-cover rounded-4xl mb-4 hover:scale-110"
              @click="
                (category = 'equipment'),
                  gameStart(),
                  (page = 'play'),
                  playClickSound()
              "
            />
          </div>
          <div
            id="places-content"
            class="category-item p-4 bg-orange-400 rounded-lg"
          >
            <h3 class="text-4xl font-bold text-gray-800 mb-4">Countries</h3>
            <img
              src="./assets/imgs/category/country.png"
              alt="Places"
              class="w-[100%] h-100 object-cover rounded-4xl mb-4 hover:scale-110"
              @click="
                (category = 'country'),
                  gameStart(),
                  (page = 'play'),
                  playClickSound()
              "
            />
          </div>
        </div>
        <div class="flex space-x-1 items-center">
          <div class="btn-back">
            <button
              @click="(page = 'home'), playClickSound()"
              class="mt-15 px-8 md:px-12 h-28 rounded-full text-6xl text-purple-700 bg-white duration-200 ease-in hover:cursor-pointer hover:bg-red-500 hover:text-white hover:font-medium"
            >
              Back
            </button>
          </div>
        </div>
      </div>
    </section>

    <section v-show="page === 'play'" class="playgame-page">
      <div
        class="playgame-container w-full bg-linear-to-r from-purple-500 to-pink-600"
      >
        <div
          v-show="modal === 'show'"
          class="show-modal w-full h-screen flex justify-center fixed z-10 bg-black/50"
        >
          <div class="modal-slide w-0 h-[30%] self-center bg-white/90 ]">
            <div v-show="modalContent === 'show'" class="modal-content">
              <h1 v-show="stateAnswer === 'correct'" class="pt-8 w-fit mx-auto text-8xl text-green-600">
                Correct
              </h1>
              <h1 v-show="stateAnswer === 'incorrect'" class="pt-8 w-fit mx-auto text-8xl text-red-600">
                Incorrect
              </h1>
              <p
                v-show="stateAnswer === 'correct'"
                class="w-fit mx-auto my-4 text-2xl text-red-400"
              >
                {{ complimentText }}
              </p>
              <p
                v-show="stateAnswer === 'incorrect'"
                class="w-fit mx-auto my-4 text-3xl text-black"
              >
                Answer: <span class="text-red-500">{{ answer }}</span>
              </p>
              <div class="btn-next flex justify-center">
                <button
                  @click="nextRound(), playClickSound()"
                  class="h-20 w-40 my-3 py-2 rounded-4xl text-2xl text-black bg-yellow-300 duration-200 ease-in hover:scale-110 hover:cursor-pointer"
                >
                  Next
                </button>
              </div>
            </div>
          </div>
        </div>
        <div class="game-content w-full h-screen">
          <header class="flex h-24">
            <div class="btn-back flex-1 self-center">
              <button
                @click="clearGame(), (page = 'category'), playClickSound()"
                class="w-40 mx-6 py-3 rounded-4xl text-2xl text-purple-700 bg-white duration-200 ease-in hover:cursor-pointer hover:bg-red-500 hover:text-white hover:font-medium"
              >
                Back
              </button>
            </div>
            <div class="timer self-center">
              <h1 class="text-4xl text-yellow-400 drop-shadow-lg font-bold">
                {{ time }}
              </h1>
            </div>
            <div class="round flex-1 self-center">
              <h1
                class="h-full mx-7 text-4xl text-end drop-shadow-lg font-bold"
              >
                {{ round }} / 15
              </h1>
            </div>
          </header>
          <div class="img-answer mt-15 my-5">
            <img
              :src="`/imgs/${category}s/${answer}.jpg`"
              :alt="`img-${answer}`"
              class="w-lg h-80 mx-auto object-cover border-[1px] hover:scale-110 duration-150 hover:cursor-zoom-in"
            />
          </div>
          <h1 class="question my-14 text-7xl text-center font-medium">
            What is {{ category }} ?
          </h1>
          <div class="choice-list flex justify-around mt-28">
            <button
              v-for="(choice, index) in choiceList"
              :key="index"
              @click="
                stopTimer(setintervalTimerId),
                  checkAnswer(index),
                  showmodal(),
                  playClickSound()
              "
              class="w-70 h-30 mx-5 py-4 rounded-4xl bg-zinc-100/70 text-5xl text-black duration-200 ease-in hover:scale-125 hover:text-white hover:cursor-pointer hover:font-medium"
              :class="getColorButton(index)"
            >
              {{ choice }}
            </button>
          </div>
        </div>
      </div>
    </section>

    <section
      class="score-page h-screen bg-linear-to-r from-fuchsia-600 to-blue-800 flex justify-center items-center border-30 rounded-lg"
      v-show="page === 'score'"
    >
      <div class="score-container text-4xl text-center">
        <h1 class="text-white text-9xl">{{ showtext() }}</h1>
        <h1
          class="py-20 text-yellow-300 text-5xl font-bold [font-family:'Lucida_Console',monospace]"
        >
          YOUR SCORE
        </h1>
        <div class="show-user-score">
          <span class="rounded-full text-5xl px-30 py-8 bg-gray-100 text-black"
            >{{ score }} / 15</span
          >
        </div>
        <div class="mt-35 flex justify-center gap-30">
          <button
            @click="clearGame(), (page = 'home'), playClickSound()"
            class="outline justify-center text-center [transition:_all_.3s_ease] leading-tight bg-white hover:bg-yellow-400 hover:text-white hover:ring-white hover:ring-3 transition-all w-auto rounded-full px-8 md:px-12 h-25 text-6xl text-purple-500 mb-6 drop-shadow-lg uppercase hover:cursor-pointer"
          >
            HOME
          </button>
          <button
            @click="clearGame(), gameStart(), (page = 'play'), playClickSound()"
            class="outline justify-center text-center [transition:_all_.3s_ease] leading-tight bg-white hover:bg-green-400 hover:text-white hover:ring-white hover:ring-3 transition-all w-auto rounded-full px-8 md:px-12 h-25 text-6xl text-purple-500 mb-6 drop-shadow-lg uppercase hover:cursor-pointer"
          >
            PLAY AGAIN
          </button>
          <video
            autoplay
            muted
            loop
            class="background-video-last absolute inset-0 w-full h-full object-cover mix-blend-screen"
          >
            <source src="./assets/video/Sequence4.webm" type="video/webm" />
          </video>
        </div>
      </div>
    </section>
  </div>
</template>


<style scoped>
.background-video-first,
.background-video-second,
.background-video-last {
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
