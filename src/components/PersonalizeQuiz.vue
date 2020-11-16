<template>
  <v-container class="flex-grow-1 d-flex flex-column">
    <v-row class="mt-3">
      <v-col>
        <v-slider
          v-model="ex3.val"
          :label="ex3.label"
          :thumb-color="ex3.color"
          :min="1"
          :max="20"
          thumb-label="always"
        ></v-slider>
      </v-col>
    </v-row>
    <v-row>
      <v-col>
        <v-select
          :items="categories"
          filled
          dense
          label="Category"
          item-text="text"
          :item-value="'value'"
          v-model="value"
        ></v-select>
      </v-col>
    </v-row>
    <v-row class="flex-column align-center">
      <p class="display-0">Select Difficulty</p>
      <v-radio-group row v-model="difficulty" class="mt-0">
        <v-radio label="Easy" value="easy"></v-radio>
        <v-radio label="Medium" value="medium"></v-radio>
        <v-radio label="Hard" value="hard"></v-radio>
      </v-radio-group>
    </v-row>

    <v-row justify="center" class="mt-6">
      <v-btn class="mr-4" color="success" @click="submitForm">Fetch My Quiz</v-btn>
      <v-btn color="error" @click="reset">clear</v-btn>
    </v-row>
  </v-container>
</template>

<script>
export default {
  name: "PersonalizeQuiz",
  data() {
    return {
      ex3: { label: "Number Of Questions", val: 10, color: "red" },
      difficulty: null,
      categories: [],
      category: null,
      value: null
    };
  },
  props: {
    url: String
  },
  async mounted() {
    let response = await fetch("https://opentdb.com/api_category.php");
    let data = await response.json();
    data.trivia_categories.sort((a, b) => (a.name > b.name ? 1 : -1));
    this.categories = data.trivia_categories.map(a => ({
      value: a.id,
      text: a.name
    }));
    this.categories.unshift({ value: "any", text: "Any Category" });
  },
  methods: {
    submitForm() {
      this.url = this.url + this.ex3.val;
      if (this.value) {
        this.url += "&category=" + this.value;
      }
      if (this.difficulty) {
        this.url += "&difficulty=" + this.difficulty.toLowerCase();
      }
      this.url += "&type=multiple";
      // console.log(url);
      this.$emit("submitForm", this.url);
    },
    reset() {
      this.ex3.val = 10;
      this.difficulty = null;
      this.value = null;
    }
  }
};
</script>