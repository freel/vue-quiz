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
  </div>
</template>


<script>
export default {
  name: "QuizAnswer",
  props: [
    "value",
    "answers",
    "question",
    "answerContainerClass",
    "answerClass",
    "answerControlClass",
    "answerCheckboxClass",
    "answerLabelClass"
  ],
  data() {
    return {
      checkedAnswers: []
    };
  },
  watch: {
    question: function() {
      this.checkedAnswers = this.value != null ? this.value : [];
    }
  }
};
</script>
