<template>
  <div :class="answerContainerClass">
    <div
      v-for="(answer, index) in answers"
      :key="index">
        <div :class="answerClass">
          <div :class="answerControlClass">
            <input
              type="checkbox"
              v-model="checkedAnswers"
              v-on:change="$emit('input', checkedAnswers)"
              :value="index"
              :class="answerCheckboxClass"
              :id="'checkbox_' + index">
            <label
              type="text"
              :class="answerLabelClass"
              :for="'checkbox_' + index">{{ answer.text }}</label>
          </div>
        </div>
    </div>
    <pre>{{ checkedAnswers }}</pre>
  </div>
</template>


<script>
export default {
  name: "Answer",
  props: {
    value: {
      type: Array
    },
    answers: {
      type: Array
    },
    question: {
      type: Number
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
  },
  data (){
    return{
      checkedAnswers: [],
    }
  },
  watch: {
    question: function (val) {
      console.log("eee");
      this.checkedAnswers = this.value != null ? this.value : []
    }
  }
}
</script>
