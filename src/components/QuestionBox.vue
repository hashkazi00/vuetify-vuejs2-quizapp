<template>
  <v-card class="fill-height primary lighten-3 rounded-0" flat>
    <v-card-title class="justify-center">
      <span v-html="currQuestion.question"></span>
    </v-card-title>
    <v-divider></v-divider>
    <v-card-text class="text--primary text-center">
      <v-list dense>
        <v-list-item-group>
          <v-list-item
            v-for="(item, i) in shuffledAnswers"
            :key="i"
            @click.prevent="selectedAnswer(i)"
            :class="answerClass(i)"
          >
            <v-list-item-title v-text="item"></v-list-item-title>
          </v-list-item>
        </v-list-item-group>
      </v-list>
    </v-card-text>

    <v-card-actions class="justify-center">
      <v-btn
        class="primary"
        text
        @click="submitAnswer"
        :disabled="selectedIndex === null || isAnswered"
        >Submit</v-btn
      >

      <v-btn class="success" @click="next" :disabled="index > 8" text
        >>Next></v-btn
      >
    </v-card-actions>
  </v-card>
</template>

<script>
import _ from "lodash";
export default {
  name: "QuestionBox",
  props: {
    currQuestion: Object,
    next: Function,
    increment: Function,
    index: Number,
  },
  data() {
    return {
      selectedIndex: null,
      shuffledAnswers: [],
      correctIndex: null,
      isAnswered: false,
    };
  },
  watch: {
    currQuestion: {
      // handler: "shuffleAnswers",
      immediate: true,
      handler() {
        this.selectedIndex = null;
        this.shuffleAnswers();
        this.isAnswered = false;
      },
    },
  },
  methods: {
    selectedAnswer(index) {
      this.selectedIndex = index;
    },
    submitAnswer() {
      let isCorrect = false;
      this.isAnswered = true;
      if (this.selectedIndex === this.correctIndex) {
        isCorrect = true;
      }
      this.increment(isCorrect); //we send the isCorrect from here to the parent and conditionally check there
    },
    shuffleAnswers() {
      let answers = [
        ...this.currQuestion.incorrect_answers,
        this.currQuestion.correct_answer,
      ];
      this.shuffledAnswers = _.shuffle(answers);
      this.correctIndex = this.shuffledAnswers.indexOf(
        this.currQuestion.correct_answer
      );
    },
    answerClass(index) {
      let answerClass = "";

      if (!this.isAnswered && this.selectedIndex === index) {
        //user sected somenthing
        answerClass = "primary lighten-3";
      } else if (this.isAnswered && this.correctIndex === index) {
        //right answer selecetd
        answerClass = "success lighten-3";
      } else if (
        this.isAnswered &&
        this.selectedIndex === index &&
        this.correctIndex !== index
      ) {
        answerClass = "error lighten-3";
      }
      return answerClass;
    },
  },
};
</script>

<style scoped></style>
