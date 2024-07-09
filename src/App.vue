<template>
 <div>
  <form >
  <label for="text" class="label"><h2>paste your text here</h2></label><br>
  <textarea  id="text" style="width: 60vw; height: 40vh" v-model="text"></textarea><br>
  <div class="container-btn">
    <button @click="uploadText" style="height: 60px; background-color: green">upload text</button>
  <button @click="uploadText" style="height: 60px; background-color: red">delete text</button>
  </div>
  </form>
  <div class="container">
       <span
       :id="`#id-${word.id}`"
       style="font-size: 32px;"
       v-for="word in createList" :key="word.id"
       @click="makeList(word)">{{ `${word.word} ` }}
       </span>
  </div>
  <div class="word-list">
    <ul>
      <li v-for="word in worldList" :key="word.id">
       <h2>
        {{ word.word }}
       </h2>
      </li>
    </ul>
  </div>
 </div>
</template>


<script>
export default {
  data() {
    return {
      text : '',
    worldList : [],
    getText : [],
    }
  },

  methods : {
   makeList(word) {
     this.worldList.push(word)
     this.worldList.find((word) => {
      if (word.id === word.id) {
        this.backgorund = true
      }
     })
   },
   uploadText(e){
    e.preventDefault()
   },
   generateId() {
      return Date.now().toString(36) + Math.random().toString(36).slice(2, 6);
    }
  },

  computed : {
    createList() {
      return this.text.split(" ").map((word) => {
        return {
          word : word,
          id : this.generateId(),
        }
      })
    },
  }, 

 
}

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
  background-color: blue;
}

.container-btn {
  display: flex;
  justify-content: center;
  gap: 100px;
}
button {
  color: white;
  font-size: 32px;
  text-transform: uppercase;
  margin-top: 30px;
}

</style>
