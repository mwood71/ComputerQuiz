<template>
  <div id="app">

    <Header
    :questionNum="this.questionNum"
    :correctNum="this.correctNum"
    />


    <QuizBox
    v-if="this.questions.length && this.endOfQuiz"
    :question="questions[index]"
    :next="next"
    :increment="increment"
    />

    <FinalResults
    v-if="!this.endOfQuiz"
    :questionNum="this.questionNum"
    :correctNum="this.correctNum"
    />


    
  </div>
</template>

<script>

import Header from './components/Header'
import QuizBox from './components/QuizBox'
import FinalResults from './components/FinalResults'
import axios from 'axios'
import 'bootstrap'
import 'bootstrap/dist/css/bootstrap.min.css'


export default {
  name: 'App',
  components: {
    Header,
    QuizBox,
    FinalResults
  },
  data() {

    return {

      questions: [],
      index: 0,
      questionNum: 0,
      correctNum: 0,
      endOfQuiz: true
    }

  },

  methods: {

    next(){

      this.index++;

      if (this.index >= this.questions.length){
        this.endOfQuiz = false
      }
    },

    increment(isCorrect){

      if (isCorrect){
        this.correctNum++
      }


      this.questionNum++

    }

  },
  mounted() {

                axios.get("https://opentdb.com/api.php?amount=10&category=18&difficulty=easy&type=multiple")
                    .then(response => {
                        this.questions = response.data.results
                        console.log(this.questions);
                        
                    })
                    .catch(function (error) {
                        console.log(error);
                    });
            }
}
</script>



