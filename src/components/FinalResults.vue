<template>
    <div class="jumbotron text-center">
        <h1 class="display-3">Final Results!</h1>
        <p v-if="this.correctNum >=7"><strong >Great Job!</strong> <br/> {{this.questionNum}} out of {{this.correctNum}} correct!</p>
        <p v-else><strong>Better Luck Next Time!</strong> <br/> {{this.correctNum}} out of {{this.questionNum}} correct.</p>
        
       
        
    </div>
</template>

<script>
export default {
  name: 'FinalResults',
  props: {
      questionNum: Number,
      correctNum: Number
  }
  
}
</script>