<script setup>
import {ref, computed} from 'vue'

const correctAnswers = ref(0)
const wrongAnswers = ref(0)
const selectedAnswer = ref(null)
const questionIndex = ref(0)
const questions = ref([
  {
    question: 'What color/colour is a polar bears skin?',
    correct_answer: 2,
    answers: [
      "White",
      "Pink",
      "Black",
      "Green"
    ],
  },
  {
    question: 'What are rhinos horn made of?',
    correct_answer: 0,
    answers: [
      "Keratin",
      "Bone",
      "Ivory",
      "Skin"
    ],
  },
  {
    question: 'What do you call a baby bat?',
    correct_answer: 3,
    answers: [
      "Cub",
      "Chick",
      "Kid",
      "Pup"
    ],
  },

])


const nextQuestion = () => {
  questionIndex.value++
  selectedAnswer.value = null
}


const setAnswer = (e) => {
  selectedAnswer.value = e.target.value
  if (selectedAnswer.value == questions.value[questionIndex.value].correct_answer) {
    correctAnswers.value++
  } else {
    wrongAnswers.value++
  }
  console.log("selectedAnswer.value ", selectedAnswer.value)
  console.log("correctAnswer.value ", correctAnswers.value)
  console.log("---")
  e.target.value = null
}


</script>

<template>
  <h1>Verisure</h1>

  <div v-if="questionIndex < questions.length">
    <div class="quiz-container">


      <p>{{ questions[questionIndex].question }}</p>
      <label v-for="(answer, index) in questions[questionIndex]['answers']" :for="index" class="answer">
        <input
            type="radio"
            :id="index"
            :value="index"
            v-model="selectedAnswer"
            @change="setAnswer($event)"
            :disabled="selectedAnswer"/> {{ answer }}

      </label>
      <button @click="nextQuestion" :disabled="!selectedAnswer">
        {{ questionIndex == questions.length - 1 ? 'Finish' : selectedAnswer == null ? 'Select an option' : 'Next' }}
      </button>
      <section>
        <p>Score is {{ correctAnswers }} / {{ questions.length }}</p>
      </section>
    </div>
  </div>
  <div v-else>
    <button @click="resetQuiz">Reset Quiz</button>
  </div>


</template>


<style>
.quiz-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  background: lightgrey;
  width: 500px;
  height: 500px;
  margin: auto;
}

.answer {
  width: 300px;
  padding: 20px;
  margin: 1px 0;
  background: silver;
  border: 1px solid silver;
}

.answer:hover {
  background: lightgrey;
  cursor: pointer;
  border: 1px solid grey;
}

button {
  margin: 20px 0 0 0;
  padding: 20px;
  width: 342px;
}
</style>
