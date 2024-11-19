<template>
    <v-container>

        <v-card class="mx-auto" max-width="344" hover>
            <v-card-item>
                <v-card-title>
                    Card title
                </v-card-title>
                <v-list-item v-for="n in 3" :key="n">{{ n }}</v-list-item>
            </v-card-item>
            <v-container>
            <v-row>
                <v-col align="center">
                    <v-btn color="primary">Submit</v-btn>
                </v-col>
                <v-col align="end">
                    <v-btn color="success">Next</v-btn>
                </v-col>
            </v-row>
        </v-container>
        </v-card>
    </v-container>
</template>
