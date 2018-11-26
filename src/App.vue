<template>
  <div>
    <form>
      <Question
      action="#"
      v-bind:question="question.text"
      :containerClass="containerClass"
      :questionClass="questionClass"
      >
        <Answer
          :answerContainerClass="answerContainerClass"
          :answerClass="answerClass"
          :answerControlClass="answerControlClass"
          :answerCheckboxClass="answerCheckboxClass"
          :answerLabelClass="answerLabelClass"
          slot="Answer"
          v-model="answered"
          v-bind:answers="question.answers"
          v-bind:question="question.id"
        >
        </Answer>
      </Question>
      <input :class="submitClass" type="button" @click="formSubmit" value="Ответить">
    </form>
  </div>
</template>

<script>
import Question from './components/Question.vue'
import Answer from './components/Answer.vue'

export default {
  name: 'vue-quiz',
  components: {
    Question,
    Answer
  },
  props: {
    questions: {
      type: Array
    },
    containerClass: {
      type: String
    },
    questionClass: {
      type: String
    },
    answerContainerClass: {
      type: String
    },
    answerClass: {
      type: String
    },
    answerControlClass: {
      type: String
    },
    answerCheckboxClass: {
      type: String
    },
    answerLabelClass: {
      type: String
    },
    submitClass: {
      type: String
    },
  },
  data () {
    return {
        page: 1,
        answered: null,
    }
  },
  computed: {
    pages: function() {
      return this.questions.length
    },
    question: function() {
      return this.questions[this.page-1]
    },
  },
  methods: {
    formSubmit: function() {
      this.$http.post(this.action, {"answers":this.answered})
      .then((response) => {
        document.write(response.body)
      })
    },
  }
}
</script>
