<template>
  <div>
  <b-nav>
    <b-nav-item disabled>Quiz App</b-nav-item>
    <b-nav-item disabled>Score:{{numCorrect}}/{{numTotal}}</b-nav-item>
    
  </b-nav>
</div>
</template>

<script>
export default {
  props: [
    'numCorrect',
    'numTotal'
  ]
}
</script>