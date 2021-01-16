<template>
  <v-app>
    <div class="editor d-print-none">
      <h1 class="text-h3 text-center mb-5">Editor</h1>
      <v-text-field
        v-model="title"
        label="Title"
        outlined
        color="#715DD6"
      ></v-text-field>
      <v-btn depressed color="#00B36F" dark @click="print()">
        Print
      </v-btn>
    </div>
    <div class="sheet">
      <h1 class="text-h3 text-center">{{ title }}</h1>
      <div class="field">
        <div class="label">Name</div>
        <div class="space"></div>
      </div>
      <p class="mt-10">Please match the words below with its definition</p>
      <div class="wrap">
        <ol class="words" type="1">
          <li v-for="(item, index) in list" :key="index">
            {{ item.word }}

            <v-btn class="d-print-none" depressed @click="remove(index)">
              Remove
            </v-btn>
          </li>
        </ol>
        <ol class="definitions" type="A">
          <li v-for="(item, index) in list" :key="index">
            {{ item.definition }}
          </li>
        </ol>
        <div class="new-word d-print-none">
          <v-text-field
            v-model="word"
            label="Word"
            outlined
            color="#715DD6"
          ></v-text-field>
          <v-text-field
            v-model="definition"
            label="Definition"
            outlined
            color="#715DD6"
          ></v-text-field>
          <v-btn depressed color="#00B36F" dark @click="add()">
            Add
          </v-btn>
        </div>
      </div>
    </div>
  </v-app>
</template>

<script>
export default {
  name: "App",

  components: {},

  data: () => ({
    title: "Matching Worksheet",
    word: "",
    definition: "",
    list: []
  }),

  methods: {
    print() {
      window.print();
    },
    add() {
      this.list.push({ word: this.word, definition: this.definition });
      this.word = "";
      this.definition = "";
    },
    remove(index) {
      this.list.splice(index, 1);
    }
  }
};
</script>

<style scoped lang="scss">
.sheet {
  font-family: "Open Sans", sans-serif;
  padding: 50px;
  max-width: 1000px;
  border: 1px solid #e6e6e6;
  margin: 50px auto;
  width: 100%;

  @media print {
    padding: 0;
    margin: 0;
    border: 0;
  }

  .field {
    display: flex;
    height: 40px;
    align-items: center;
    max-width: 500px;
    margin-top: 70px;

    .label {
      color: black;
    }
    .space {
      border-bottom: 2px solid black;
      flex: 1;
      margin-left: 16px;
      height: 100%;
    }
  }
}

.wrap {
  display: flex;
  flex-wrap: wrap;
}

.words {
  width: 40%;
}

.definitions {
  width: 60%;
}

li {
  padding: 8px 0;
  min-height: 45px;
}

.editor {
  max-width: 1000px;
  width: 100%;
  margin: 0 auto;
  padding: 30px 0;

  h1 {
    color: #dc3545;
  }
}

.new-word {
  width: 100%;
  max-width: 410px;
  background: #f7f7f7;
  padding: 20px;
  margin-top: 30px;
  border-radius: 10px;
}
</style>
