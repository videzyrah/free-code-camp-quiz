<template>
  <div>
  <b-jumbotron>
    <!--
    <template v-slot:header>BootstrapVue</template>
    -->

    <template v-slot:lead>
      {{currentQuestion.question}}
    </template>

    <hr class="my-4">
    <b-list-group>
      <b-list-group-item
        v-for="(answer, index) in answers" 
        :key="index"
        @click.prevent="selectAnswer(index)"
        :class="[
          !answered && selectedIndex === index ? 'selected' :
          answered && correctIndex === index  ? 'correct' : 
          answered && selectedIndex === index && correctIndex !== index  ? 
          'incorrect' : ''
          ]"
      >
      {{ answer }}
      </b-list-group-item>
    </b-list-group>
  
    <b-button 
      variant="primary"
      @click="submitAnswer"
      :disabled="selectedIndex === null || answered">
      Submit
    </b-button>
    <b-button @click="next" variant="success">
      Next
    </b-button>
  </b-jumbotron>
  </div>
</template>

<script>
export default {
  props:{
    currentQuestion: Object,
    next: Function,
    increment: Function
  },
  data(){
    return{
    answers: [],
    selectedIndex: null,
    correctIndex: null,
    answered: false
  
    }
  },
  //computed: {
    //answers(){
      //let answers = [...this.currentQuestion.incorrect_answers]
      //answers.push(this.currentQuestion.correct_answer)
      //this.correctIndex = answers.length
      //return answers
    //}
  //},
  watch: { 
    currentQuestion: {
      immediate: true,
      handler() {
        this.selectedIndex = null
        this.answered = null
        this.getAnswers()
      }
    } 
  },
  methods:{
    getAnswers(){
      let answers = [...this.currentQuestion.incorrect_answers]
      answers.push(this.currentQuestion.correct_answer)
      this.correctIndex = (answers.length -1)
      this.answers = answers
    },
    selectAnswer(index){
      this.selectedIndex = index
    },
    submitAnswer(){
      let isCorrect = false

      if (this.selectedIndex === this.correctIndex){
        isCorrect = true
      }
      this.increment(isCorrect)
      this.answered = true
    }
  },
}
</script>
<style scoped>
  .list-group {
    margin-bottom: 15px;
  }
  .list-group-item:hover {
    background: gray;
    cursor: pointer;
  }
  .btn {
    margin: 0 5px;
  }
  .selected {
    background-color: lightblue;
  }
  .correct{
    background-color:lightgreen;
  }
  .incorrect{
    background-color:red;
  }
</style>