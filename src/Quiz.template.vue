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
            <div v-if="formInvalid && isCorrect === null" class="border-yellow-700 border-8 w-full items-center flex justify-center bg-yellow-600 mr-4">{{formInvalid}}</div>
            <div v-if="isCorrect" class="border-green-700 border-8 w-full items-center flex justify-center bg-green-600 mr-4">Correct !</div>
            <div v-else-if="!isCorrect && isCorrect != null" class="border-red-700 border-8 w-full items-center flex justify-center bg-red-600 mr-4">Incorrect !</div>
            <button v-if="isCorrect === null" class="border-2 rounded bg-blue-600 p-4 hover:bg-blue-900" type="submit">Submit</button>
            <button v-else class="border-2 rounded bg-blue-600 p-4 hover:bg-blue-900" type="button" @click="nextQuestion">Next</button>
          </div>
        </div>
      </div>
    </form>

    <span>Your final score : {{totalCorrectResponse}} / {{questions.length}}</span>

  </div>
</template>

<script setup>
import { ref } from "vue";

const picked = ref()
const questionNumber = ref(0)
const totalCorrectResponse = ref(0)
const isCorrect = ref(null)
const formInvalid = ref('')

function registerAnswer(answer) {
  const goodAnswer = questions[questionNumber.value].answer

  if (answer) {
    console.log(answer)
    if (answer === goodAnswer) {
      isCorrect.value = true;
      totalCorrectResponse.value++;
    } else {
      isCorrect.value = false;
    }
  } else {
    formInvalid.value = 'please select one response'
  }
}

function nextQuestion() {
  isCorrect.value = null
  formInvalid.value = ''
  questionNumber.value++
}

const questions = [
  {
    question: "Is the following code block valid?\nconst count = reactive(0);",
    options: ["Yes", "No"],
    answer: "No"
  },
  {
    question: "v-model is useful for...",
    options: ["one-way data binding", "two-way data binding", "transporting elements to the body", "looping over data"],
    answer: "two-way data binding"
  },
  {
    question: "What is the advantage of using scoped slots in Vue components?",
    options: [
      "They provide better performance than regular slots",
      "Allows the slot's content to make use of data from both the parent scope and the child scope",
      "They allow easier dynamic styling of the slot content",
      "All of the above"
    ],
    answer: "Allows the slot's content to make use of data from both the parent scope and the child scope"
  },
  {
    question: "The following code block will always render the current date and time, accurate to the second.\n&lt;script setup&gt;\n  import { computed } from \"vue\";\n  const now = computed(() =&gt; new Date());\n&lt;/script&gt;\n\n&lt;template&gt; {{ now }} &lt;/template&gt;",
    options: ["True", "False"],
    answer: "False"
  },
  {
    question: "Which Vue directive is used for rendering a list of items?",
    options: ["v-list", "v-array", "v-foreach", "v-for"],
    answer: "v-for"
  },
  {
    question: "The Transition component is useful for animating the insertion, removal, and order change of elements that are rendered in a list.",
    options: ["True", "False"],
    answer: "False"
  },
  {
    question: "Watchers and computed properties are 2 different solutions to the same problem.",
    options: ["True", "False"],
    answer: "False"
  },
  {
    question: "What will the following Vue code render as HTML?\n&lt;script setup&gt;\n  import { ref } from \"vue\";\n  const url = ref(\"https://vueschool.io\");\n  const attributeName = ref(\"href\");\n&lt;/script&gt;\n&lt;template&gt;\n  &lt;a :[attributeName]=\"url\"&gt; ... &lt;/a&gt;\n&lt;/template&gt;",
    options: [
      "<a href=\"https://vueschool.io\"> ... </a>",
      "<a attributeName=\"https://vueschool.io\"> ... </a>",
      "<a link=\"https://vueschool.io\"> ... </a>",
      "This code is invalid and will throw an error"
    ],
    answer: "<a href=\"https://vueschool.io\"> ... </a>"
  },
  {
    question: "Given the following component defintion and subsequent use, will the word \"Submit\" render to the page?\n// MyButton.vue\n&lt;template&gt;\n  &lt;button&gt;&lt;slot&gt;Submit&lt;/slot&gt;&lt;/button&gt;\n&lt;/template&gt;\n// Usage in parent component\n\n&lt;MyButton&gt;Click Me&lt;/MyButton&gt;",
    options: ["Yes", "No"],
    answer: "No"
  },
  {
    question: "It is possible to validate component event payloads at runtime.",
    options: ["True", "False"],
    answer: "True"
  },
  {
    question: "Vuejs has an official chrome extension for developers.",
    options: ["True", "False"],
    answer: "True"
  },
  {
    question: "v-model is useful for...",
    options: ["one-way data binding", "two-way data binding", "transporting elements to the body", "looping over data"],
    answer: "two-way data binding"
  },
  {
    question: "Using v-html comes with some security risks and should be used cautiously.",
    options: ["True", "False"],
    answer: "True"
  },
  {
    question: "Given this component defintion, which of the following is a valid usage?\n// MyComponent.vue\n&lt;script setup&gt;\n  defineProps({\n    items: Array,\n    active: Boolean,\n  });\n&lt;/script&gt;\n\n&lt;template&gt;...&lt;/template&gt;",
    options: [
      "<MyComponent active=\"Yes\" />",
      "<MyComponent active=\"false\" />",
      "<MyComponent active=\"[]\" />",
      "<MyComponent active />"
    ],
    answer: "<MyComponent active />"
  },
  {
    question: "Template refs are useful for...",
    options: [
      "defining reactive state",
      "increasing component performance",
      "directly accessing DOM elements",
      "cleaning up side-effects like timers"
    ],
    answer: "directly accessing DOM elements"
  },
  {
    question: "The following 2 code blocks will render the exact same thing.\n&lt;script setup&gt;\n  const html = \"&lt;p&gt;&lt;/p&gt;\";\n&lt;/script&gt;\n&lt;template&gt;\n  &lt;div&gt;{{ html }}&lt;/div&gt;\n&lt;/template&gt;\n&lt;script setup&gt;\n  const html = \"&lt;p&gt;&lt;/p&gt;\";\n&lt;/script&gt;\n&lt;template&gt;\n  &lt;div v-html=\"html\"&gt;&lt;/div&gt;\n&lt;/template&gt;",
    options: ["True", "False"],
    answer: "False"
  },
  {
    question: "The following code block will always render the current date and time, accurate to the second.\n&lt;script setup&gt;\n  import { computed } from \"vue\";\n  const now = computed(() =&gt; new Date());\n&lt;/script&gt;\n\n&lt;template&gt; {{ now }} &lt;/template&gt;",
    options: ["True", "False"],
    answer: "False"
  },
  {
    question: "Given the following code block what is the most appropriate value to pass to ref()\n&lt;script setup&gt;\n  const data = ref(/*what value goes here?*/);\n&lt;/script&gt;\n\n&lt;template&gt; &lt;input type=\"checkbox\" v-model=\"data\" /&gt; I agree &lt;/template&gt;",
    options: ["1", "true", "Yes", "null"],
    answer: "null"
  },
  {
    question: "When defining data with the reactive() function, you must access it's value with .value",
    options: ["True", "False"],
    answer: "False"
  },
  {
    question: "What the is the shorthand for v-on",
    options: ["@", ":", "&", "#"],
    answer: "@"
  }
];
</script>
