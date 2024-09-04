<template>
  <div class="w-full h-full flex justify-center items-center flex-col">
    <form @submit.prevent="registerAnswer(picked)">
      <div v-for="(question, index) in questions">
        <div v-if="index === questionNumber">
          <h1 class="font-bold text-4xl underline underline-offset-8">{{ question.question }}</h1>
          <div v-for="answer in question.options" class="my-6 text-3xl">
            <input  required type="radio" :id="answer" :value="answer" v-model="picked" class="mr-4">
            <label :for="answer">{{ answer }}</label>
          </div>
          <div class="flex flex-row w-full justify-between">
            <div v-if="isCorrect" class="border-green-700 border-8 w-full items-center flex justify-center bg-green-600 mr-4">Correct !</div>
            <div v-else-if="!isCorrect && isCorrect != null" class="border-red-700 border-8 w-full items-center flex justify-center bg-red-600 mr-4">Incorrect !</div>
          <button class="border-2 rounded bg-blue-600 p-4 hover:bg-blue-900" type="submit">Submit</button>
          </div>
        </div>
      </div>
    </form>

    <span>totalCorrectResponse : {{totalCorrectResponse}}</span>

  </div>
</template>

<script setup>
import { ref } from "vue";

const picked = ref()
const questionNumber = ref(0)
const totalCorrectResponse = ref(0)
const isCorrect = ref()

function registerAnswer(answer) {

  const goodAnswer = questions[questionNumber.value].answer
  if (answer === goodAnswer) {
    isCorrect.value = true
    totalCorrectResponse.value++
  } else {
    isCorrect.value = false
  }
  console.log({ goodAnswer })
  console.log('Answer selected', answer)
  // questionNumber.value++
}

const questions = [
  {
    question: "What is the capital of France?",
    options: ["London", "Berlin", "Paris", "Rome"],
    answer: "Paris",
  },
  {
    question: "Which planet is closest to the sun?",
    options: ["Earth", "Mars", "Venus", "Mercury"],
    answer: "Mercury",
  },
  {
    question: "What is the largest mammal?",
    options: ["Elephant", "Blue Whale", "Giraffe", "Hippopotamus"],
    answer: "Blue Whale",
  },
  {
    question: "What is the largest planet in our solar system?",
    options: ["Earth", "Jupiter", "Saturn", "Neptune"],
    answer: "Jupiter",
  }
];
</script>
