<template>
    <v-container>
        <v-app-bar :elevation="2" color="warning">
            <v-col>
                <v-app-bar-title>Quiz Time</v-app-bar-title>
            </v-col>
            <v-col>
                <p>Counter: {{ correctGuesses }}/ {{ totalGuesses }}</p>
            </v-col>
        </v-app-bar>
    </v-container>
</template>
<script>
export default {
    props: {
        correctGuesses: Number,
        totalGuesses: Number
    }
}
</script>