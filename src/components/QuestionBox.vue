<template>
    <v-container>
        <v-card class="mx-auto" max-width="600" hover>
                <v-card-title>
                    {{ currentQuestion.question }}
                </v-card-title>
                <v-list-item :class="{selected: index === selectedIndex, answer: true}" @click="selectAnswer(index)" v-ripple v-for="(answer, index) in answers" :key="index">{{ answer }}</v-list-item>
            <v-container>
            <v-row>
                <v-col align="start">
                    <v-btn color="primary">Submit</v-btn>
                </v-col>
                <v-col align="end">
                    <v-btn @click="increment" color="success">Next</v-btn>
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
        increment: Function
    },
    data() {
        return {
            selectedIndex: null
        }
    },
    computed: {
        answers(){
            return [...this.currentQuestion.incorrect_answers, this.currentQuestion.correct_answer];
        }
    },
    watch: {
        currentQuestion() {
            this.selectedIndex = null;
            this.shuffleAnswers();

        }

    },
    methods: {
        selectAnswer: function(index) {
            this.selectedIndex = index;
        },
        shuffleAnswers: function() {
            let answers = [...this.currentQuestion.incorrect_answers, this.currentQuestion.correct_answer];
            return _.shuffle(answers);
        }
    }
}

</script>

<style scoped>
.selected {
    border: 1px solid #0091EA;
}
.correct {
    background-color: #008000;
}

.incorrect {
    background-color: #ff0000;
}

.answer:hover {
    cursor: pointer;
}

</style>