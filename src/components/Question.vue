<template>
  <keep-alive>
    <div>
      <span
        :class="questionClass">{{ question }}</span>
      <slot
        name="Answer"></slot>
    </div>
  </keep-alive>
</template>


<script>
export default {
  name: "Question",
  props: {
    question:{
      type: String
    },
    startPage:{
      type: Number,
      default: 0,
    },
    action:{},
    timer:{},
    containerClass: {
      type: String
    },
    questionClass: {
      type: String
    }
  },
}
</script>
