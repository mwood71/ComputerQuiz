<template>
    <div>
        <div class="text-center container" style="margin-top: 58px;">

            <div class="row">
                <div class="col-6 offset-3">
                    <h4 class="mb-3">{{question.question}}</h4>
                    <ul class="list-group mb-4 mt-4">

                        <li v-for="(answer,index) in answers" :key="index" @click="selectAnswer(index)"
                            class="list-group-item" :class="answerClass(index)">{{answer}}</li>

                    </ul>
                    <button @click="submit()" class="btn btn-primary mr-1">Submit</button>
                    <button @click="next()" class="btn btn-success ml-1">Next</button>

                </div>

            </div>

        </div>
    </div>
</template>

<script>
    export default {
        name: 'QuizBox',
        props: {
            question: Object,
            next: Function,
            increment: Function

        },
        data() {

            return {
                selectedIndex: null,
                answers: [],
                correctIndex: null,
                answered: false,
                isCorrect: false

            }

        },
        watch: {
            question: {
                immediate: true,
                handler() {
                    this.selectedIndex = null
                    this.answered = false
                    this.shuffleAnswers()
                }
            }
        },

        methods: {

            selectAnswer(index) {

                this.selectedIndex = index;

            },

            shuffleAnswers() {

                let answers = [...this.question.incorrect_answers];
                answers.push(this.question.correct_answer);

                for (let i = answers.length - 1; i > 0; i--) {
                    const j = Math.floor(Math.random() * i)
                    const temp = answers[i]
                    answers[i] = answers[j]
                    answers[j] = temp
                }

                this.answers = answers;
                this.correctIndex = this.answers.indexOf(this.question.correct_answer);

            },

            answerClass(index) {

                let answerClass = ''

                if (!this.answered && this.selectedIndex === index){
                    answerClass = 'selected'
                }
                else if (index === this.correctIndex && this.answered) {
                    answerClass = 'correct'
                } else if (index === this.selectedIndex && this.selectedIndex != this.correctIndex && this.answered) {
                    answerClass = 'incorrect'
                }
                return answerClass

            },
            submit() {

                if (this.selectedIndex === this.correctIndex) {

                    this.isCorrect = true

                }
                this.increment(this.isCorrect)
                this.answered = true
                

            }


        },

    }
</script>

<style scoped>
    .list-group-item {
        cursor: pointer;
    }

    .list-group-item:hover {
        background-color: lightgrey;
    }

    .correct {
        background-color: green;
    }

    .selected {
        background-color: grey;
    }

    .incorrect {
        background-color: red;
    }
</style>