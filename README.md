# vue-quiz

Vue.js base Quiz plugin, with multiple answers and other features.
One question per page.

## Project setup
```
npm install freel/vue-quiz
```

## Use with Nuxt
```
<template>
  <vue-quiz
    *param*
  />
</template>

<script>
import VueQuiz from 'vue-quiz'

export default {
  components: {
    VueQuiz
  }
}
</script>
```

## Props
|Name            | Type | Description
| --- | --- | --- |
|container-class | String | CSS class names for top layout
|question-class  | String | CSS class names for question layout
|answers-container-class | String | CSS class names for answers layout
|answer-class | String | CSS class names for answer block
|answer-control-class | String | CSS class names for answer custom form control
|answer-checkbox-class | String | CSS class names for answer checkbox
|answer-label-class | String | CSS class names for answer label
|submit-class | String | CSS class names for submit button
