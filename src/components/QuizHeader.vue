<template>
    <v-container>
        <v-app-bar :elevation="2" color="warning">
            <v-col>
                <v-app-bar-title>Quiz Time</v-app-bar-title>
            </v-col>
            <v-col>
                <p>Counter: {{ counter + 1 }}/10</p>
            </v-col>
        </v-app-bar>
    </v-container>
</template>
<script>
export default {
    props: {
        counter: Number
    }
}
</script>