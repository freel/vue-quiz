<template>
  <div>
    <form>
      <Question
      :action="action"
      :question="question.text"
      :containerClass="containerClass"
      :questionClass="questionClass"
      >
        <Answer
          slot="Answer"
          v-model="answered[item]"
          :answerContainerClass="answerContainerClass"
          :answerClass="answerClass"
          :answerControlClass="answerControlClass"
          :answerCheckboxClass="answerCheckboxClass"
          :answerLabelClass="answerLabelClass"
          :answers="question.answers"
          :question="item"
        >
        </Answer>
      </Question>
      <!-- <input type="button" @click="prevousItem" value="Back"> -->
      <input v-show="isNextEnabled" :class="nextClass" type="button" @click="nextItem" :value="nextValue">
      <input v-show="isSubmitEnabled" :class="submitClass" type="button" @click="formSubmit" :value="submitValue">
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
      type: Array,
      default: () => { return [
        {text:"Vue.JS is",
        answers:[{text:"JS framework"},{text:"PHP framework"},{text:"Something from space"}]},
        {text:"This is second question?",
        answers:[{text:"Yes"},{text:"No"},{text:"Both"}]},
        {text:"This is third question?",
        answers:[{text:"Yes!"},{text:"No!"},{text:"Both?"}]},
      ]}
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
    submitValue: {
      type: String,
      default: "Submit"
    },
    submitEnabled: {
      type: Boolean,
      default: false
    },
    nextClass: {
      type: String
    },
    nextValue: {
      type: String,
      default: "Next"
    },
    nextEnabled: {
      type: Boolean,
      default: false
    },
    action: {
      type: String,
      default: "#"
    },
  },
  data () {
    return {
        item: 0,
        answered: [],
    }
  },
  computed: {
    pages: function() {
      return this.questions.length
    },
    question: function() {
      return this.questions[this.item]
    },
    isSubmitEnabled: function() {
      return this.submitEnabled || (this.answered != null ? this.answered.filter(String).length : 0) == this.pages
    },
    isNextEnabled: function() {
      return this.nextEnabled || (this.answered[this.item] != null ? this.answered[this.item].filter(String).length : false)
    }
  },
  methods: {
    nextItem: function() {
      return this.item++
    },
    prevousItem: function() {
      return this.item--
    },
    formSubmit: function() {
      this.$http.post(this.action, {"answers":this.answered})
      .then((response) => {
        document.write(response.body)
      })
    },
  }
}
</script>
