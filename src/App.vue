<script setup>
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
const choiceList = [];
const randomChoice = (arr) => {
  for (let i = 0; i < 5; i++) {
    const index = Math.floor(Math.random() * arr.length);
    choiceList.push(arr[index]);
    arr.splice(index, 1);
  }
};
const randomAnswer = () => {
  const index = Math.floor(Math.random() * choiceList.length);
  return choiceList[index];
};
console.log(animalList)
animalList.splice(0,1)
console.log(animalList)
animalList.splice(0,1)
console.log(animalList)
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
    </section>
    <section class="score-page">
      <!-- code here -->
    </section>
  </div>
</template>

<style scoped></style>
