<template>
    <v-container>
        <v-card class="mx-auto" max-width="600" hover>
            <v-card-title>
                {{ currentQuestion.question }}
            </v-card-title>
            <v-list-item :class="{ selected: index === selectedIndex, answer: true, correct: submitted && correctIndex === index, incorrect: submitted && selectedIndex === index && correctIndex !== index }" @click="selectAnswer(index)"
                v-ripple v-for="(answer, index) in shuffledAnswers" :key="index">{{ answer }}</v-list-item>
            <v-container>
                <v-row>
                    <v-col align="start">
                        <v-btn color="primary" @click="checkGuess" :disabled="submitted === true || selectedIndex === null">
                            Submit
                        </v-btn>
                    </v-col>
                    <v-col align="end">
                        <v-btn @click="increment" color="success" :disabled="!submitted">Next</v-btn>
                    </v-col>
                </v-row>
            </v-container>
        </v-card>
    </v-container>
</template>

<script>
import _ from "lodash";

export default {
    props: {
        currentQuestion: Object,
        increment: Function,
        updateScores: Function
    },
    data() {
        return {
            selectedIndex: null,
            correctIndex: null,
            shuffledAnswers: [],
            submitted: false
        }
    },
    computed: {
        answers() {
            return [...this.currentQuestion.incorrect_answers, this.currentQuestion.correct_answer];
        }
    },
    watch: {
        // currentQuestion() { // example of a watch function
        //     this.selectedIndex = null;
        //     this.shuffleAnswers();
        // },
        currentQuestion: {
            immediate: true,
            handler() {
                this.selectedIndex = null;
                this.submitted = false;
                this.shuffleAnswers();
            }
        }
    },
    methods: {
        selectAnswer: function (index) {
            if (this.submitted) {
                return;
            }
            this.selectedIndex = index;
        },
        shuffleAnswers: function () {
            let answers = [...this.currentQuestion.incorrect_answers, this.currentQuestion.correct_answer];
            this.shuffledAnswers = [..._.shuffle(answers)];
            this.correctIndex = this.shuffledAnswers.indexOf(this.currentQuestion.correct_answer);
        },
        checkGuess: function () {
            this.updateScores(this.selectedIndex === this.shuffledAnswers.indexOf(this.currentQuestion.correct_answer));
            this.submitted = true;
        }
    }
}

</script>

<style scoped>
.selected {
    background-color: #88d1ff;
}

.correct {
    background-color: #77da77;
}

.incorrect {
    background-color: #f19a9a;
}

.answer:hover {
    cursor: pointer;
}
</style>