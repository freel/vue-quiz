<template>
  <div>
      <keep-alive>
        <div :class="containerClass">
          <p :class="questionClass">{{ question }}</p>
          <slot name="Answer"></slot>

        </div>
      </keep-alive>
  </div>
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
