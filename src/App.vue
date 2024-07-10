<template>
  <div>
    <form>
      <label for="text" class="label"><h2>paste your text here</h2></label><br>
      <textarea id="text" style="width: 60vw; height: 40vh" v-model="text"></textarea><br>
      <div class="container-btn">
        <button @click="uploadText" style="height: 60px; background-color: green">upload text</button>
        <button @click="uploadText" style="height: 60px; background-color: red">delete text</button>
      </div>
    </form>

    <div class="container">
      <span
        :id="`id-${word.id}`"
        style="font-size: 32px;"
        v-for="word in createList"
        :key="word.id"
        @click="makeList(word)"
        :style="{ backgroundColor: findWord(word) ? 'green' : '' }"
      >
        {{ `${word.word} ` }}
      </span>
    </div>
    <div v-if="worldList.length > 0">
      <ul class="word-list">
        <li v-for="word in worldList" :key="word.id">
          <h2>{{ word.word }}</h2>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      text: '',
      worldList: [],
      getText: [],
      selectWord: '',
    };
  },

  methods: {
    makeList(word) {
      if (!this.findWord(word)) {
        this.worldList.push(word);
      }
    },

    findWord(val) {
      return this.worldList.some((word) => word.word === val.word);
    },

    uploadText(e) {
      e.preventDefault();
    },

    generateId() {
      return Date.now().toString(36) + Math.random().toString(36).slice(2, 6);
    },
  },

  computed: {
    createList() {
      return this.text.split(" ").map((word) => {
        return {
          word: word,
          id: this.generateId(),
        };
      });
    },
  },
};
</script>

<style>
form {
  padding: 40px;
  background-color: lightblue;
}

.label {
  margin: 40px;
}

textarea {
  font-size: 32px;
}

.color {
  background-color: rgb(148, 148, 245);
}

.container-btn {
  display: flex;
  justify-content: center;
  gap: 100px;
}

button {
  color: white;
  font-size: 16px;
  text-transform: uppercase;
  margin-top: 30px;
}

.word-list {
  background-color: rgb(146, 220, 146);
  width: 200px;
  padding: 20px;
  border : 3px solid black;
  text-align: center;
  list-style: decimal;
  gap: 30px;
}


</style>
