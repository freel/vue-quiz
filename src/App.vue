<template>
  <div :class="containerClass">
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
      <input
        type="button"
        v-show="isPrevousShow"
        :disabled="isPrevousDisabled"
        @click="prevousItem"
        :class="[buttonClass, nextClass]"
        :value="prevousValue">
      <input
        type="button"
        v-show="isSubmitShow"
        :disabled="isSubmitDisabled"
        @click="formSubmit"
        :class="[buttonClass, submitClass]"
        :value="submitValue">
      <input
        type="button"
        v-show="isNextShow"
        :disabled="isNextDisabled"
        @click="nextItem"
        :class="[buttonClass, nextClass]"
        :value="nextValue">
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
        answers:[{text: "JS framework"}, {text: "PHP framework"}, {text: "Something from space"}]},
        {text:"This is second question?",
        answers:[{text: "No"}, {text: "Both"}, {text:" Yes"}]},
        {text:"This is third question?",
        answers:[{text: "No!"}, {text: "Yes!"}, {text: "Both?"}]},
      ]}
    },
    containerClass: {
      type: String,
      default: "jumbotron"
    },
    questionClass: {
      type: String,
      default: "h5"
    },
    answerContainerClass: {
      type: String,
      default: "col-auto my-1"
    },
    answerClass: {
      type: String,
      default: "alert alert-dark"
    },
    answerControlClass: {
      type: String,
      default: "custom-control custom-checkbox mr-sm-2"
    },
    answerCheckboxClass: {
      type: String,
      default: "custom-control-input"
    },
    answerLabelClass: {
      type: String,
      default: "custom-control-label"
    },
    // Buttons
    buttonClass: {
      type: String,
      default: "btn btn-primary"
    },
    // Submit
    submitClass: {
      type: String,
      default: ""
    },
    submitValue: {
      type: String,
      default: "Submit"
    },
    submitShow: {
      type: Boolean,
      default: false
    },
    submitDisabled: {
      type: Boolean,
      default: true
    },
    // Next
    nextClass: {
      type: String,
      default: ""
    },
    nextValue: {
      type: String,
      default: "Next"
    },
    nextShow: {
      type: Boolean,
      default: true
    },
    // Prevous
    prevousClass: {
      type: String,
      default: ""
    },
    prevousValue: {
      type: String,
      default: "Back"
    },
    prevousShow: {
      type: Boolean,
      default: true
    },
    // Submit form action
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
    isSubmitShow: function() {
      return this.submitShow || (this.answered != null ? this.answered.filter(String).length : 0) == this.pages
    },
    isSubmitDisabled: function() {
      return this.submitDisabled && (this.answered != null ? this.answered.filter(String).length : 0) != this.pages
    },
    isNextShow: function() {
      return this.nextShow || (this.answered[this.item] != null ? this.answered[this.item].filter(String).length : false)
    },
    isNextDisabled: function() {
      return this.item >= this.pages - 1
    },
    isPrevousShow: function() {
      return this.prevousShow
    },
    isPrevousDisabled: function() {
      return this.item <= 0
    },
  },
  methods: {
    nextItem: function() {
      return this.item < this.pages ? this.item++ : void 0
    },
    prevousItem: function() {
      return this.item > 0 ? this.item-- : void 0
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
