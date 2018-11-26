<template>
  <div :class="answerContainerClass">
    <div
      v-for="answer in this.answers"
      :key="answer.id">
        <div :class="answerClass">
          <div :class="answerControlClass">
            <input type="checkbox" :class="answerCheckboxClass" v-model="checked" @change="change" v-bind:value="collect(answer.id)" v-bind:id="'checkbox_' + answer.id">
            <label type="text" :class="answerLabelClass" v-bind:for="'checkbox_' + answer.id">{{ answer.text }}</label>
          </div>
        </div>
    </div>
  </div>
</template>


<script>
    export default {
        name: "Answer",
        props: {
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
            checked: [],
          }
        },
        methods: {
          change: function(){
            this.$emit('input', this.checked);
          },
          collect(id){
            return{ [this.question]: id}
          }
        },
        computed:{
        }
    }
</script>
