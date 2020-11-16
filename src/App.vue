<template>
  <v-app>
    <v-container>
      <v-row>
        <v-col xs="12" sm="8" offset-sm="2">
          <Header :numCorrect="numCorrect" :numTotal="numTotal" />
        </v-col>
      </v-row>
      <v-row>
        <v-col xs="12" sm="8" offset-sm="2">
          <v-main>
            <PersonalizeQuiz v-if="!formSubmitted" @submitForm="submitForm($event)" :url="url" />
            <QuestionBox
              :currQuestion="questions[index]"
              :next="next"
              v-if="questions.length && formSubmitted"
              :increment="increment"
              :index="index"
              :url="url"
            />
          </v-main>
        </v-col>
      </v-row>
      <v-row>
        <v-col xs="12" sm="8" offset-sm="2">
          <Footer />
        </v-col>
      </v-row>
    </v-container>
  </v-app>
</template>

<script>
import Header from "@/components/Header";
import Footer from "@/components/Footer.vue";
import QuestionBox from "@/components/QuestionBox.vue";
import PersonalizeQuiz from "@/components/PersonalizeQuiz.vue";

export default {
  name: "App",

  components: {
    Header,
    Footer,
    QuestionBox,
    PersonalizeQuiz
  },

  data() {
    return {
      questions: [],
      index: 0,
      numCorrect: 0,
      numTotal: 0,
      formSubmitted: false,
      url: "https://opentdb.com/api.php?amount="
    };
  },
  methods: {
    next() {
      this.index++;
    },
    increment(isCorrect) {
      if (isCorrect) {
        this.numCorrect++;
      }
      this.numTotal++;
    },

    async submitForm(url) {
      this.formSubmitted = !this.formSubmitted;
      console.log(url);
      let response = await fetch(url);
      let data = await response.json();
      // console.log(result);
      this.questions = data.results;
    }
  }
  // async mounted() {
  //   //When we use fetch we need to wait to atleast one promise(MDN DOcs)
  //   // 1. First await to wait for the promise from fetch
  //   const response = await fetch(this.url, {
  //     method: "get"
  //   });
  //   // 2. Second await to wait for the promise from fetch
  //   let data = await response.json();

  //   this.questions = data.results;
  // }
};
</script>
