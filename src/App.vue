<template>
  <v-app>
    <v-main>
      <QuizHeader />
      <QuestionBox />
    </v-main>
  </v-app>
</template>

<script>
import QuizHeader from './components/QuizHeader';
import QuestionBox from './components/QuestionBox';

export default {
  name: 'App',

  components: {
    QuizHeader,
    QuestionBox,
  },

  data: () => ({
    //
  }),
};
</script>
