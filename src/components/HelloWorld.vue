<template>
  <div class="hello">
    <!-- v-text -->
    <h1>{{ msg }}</h1>
    <!--
    <p>
      For a guide and recipes on how to configure / customize this project,<br>
      check out the
      <a href="https://cli.vuejs.org" target="_blank" rel="noopener">vue-cli documentation</a>.
    </p>
    <h3>Installed CLI Plugins</h3>
    <ul>
      <li><a href="https://github.com/vuejs/vue-cli/tree/dev/packages/%40vue/cli-plugin-babel" target="_blank" rel="noopener">babel</a></li>
      <li><a href="https://github.com/vuejs/vue-cli/tree/dev/packages/%40vue/cli-plugin-eslint" target="_blank" rel="noopener">eslint</a></li>
    </ul>
    <h3>Essential Links</h3>
    <ul>
      <li><a href="https://vuejs.org" target="_blank" rel="noopener">Core Docs</a></li>
      <li><a href="https://forum.vuejs.org" target="_blank" rel="noopener">Forum</a></li>
      <li><a href="https://chat.vuejs.org" target="_blank" rel="noopener">Community Chat</a></li>
      <li><a href="https://twitter.com/vuejs" target="_blank" rel="noopener">Twitter</a></li>
      <li><a href="https://news.vuejs.org" target="_blank" rel="noopener">News</a></li>
    </ul>
    <h3>Ecosystem</h3>
    <ul>
      <li><a href="https://router.vuejs.org" target="_blank" rel="noopener">vue-router</a></li>
      <li><a href="https://vuex.vuejs.org" target="_blank" rel="noopener">vuex</a></li>
      <li><a href="https://github.com/vuejs/vue-devtools#vue-devtools" target="_blank" rel="noopener">vue-devtools</a></li>
      <li><a href="https://vue-loader.vuejs.org" target="_blank" rel="noopener">vue-loader</a></li>
      <li><a href="https://github.com/vuejs/awesome-vue" target="_blank" rel="noopener">awesome-vue</a></li>
    </ul>
    -->
    <button @click="awesome = !awesome">Toggle</button>

    <h1 v-if="awesome">Vue is awesome!</h1>
    <h1 v-else>Oh no</h1>
    <!-- v-else-if -->
    <div v-if="type === 'A'">
      A
    </div>
    <div v-else-if="type === 'B'">
      B
    </div>
    <div v-else-if="type === 'C'">
      C
    </div>
    <div v-else>
      Not A/B/C
    </div>
    <!-- v-for -->
    <!--
    <li v-for="(item, index) in items">
      {{ parentMessage }} - {{ index }} - {{ item.message }}
    </li>
    -->
    <br>
    <h2>Grüsse mich!</h2>
    <button @click="greet">Greet</button>
    <br>
    <h2>Stelle eine Frage</h2>
    <p>
      Stelle eine ja/nein Frage (auf Englisch):
      <input v-model="question" />
    </p>
    <p>{{ answer }}</p>
    <br>
    <h2>Hat Fabrizio Bücher veröffentlicht?</h2>
    <span>{{ author.books.length > 0 ? 'Ja' : 'Nein' }}</span>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data() {
    return {
      awesome: true,
      type: 'B',
      parentMessage: 'Parent',
      items: [{ message: 'Foo' }, { message: 'Bar' }],
      name: 'Vue.js',
      question: '',
      answer: 'Fragen sollten einen Fragezeichen enthalten!',
      author: {
        name: 'Fabrizio Di Leo',
        books: []
      }
    }
  },
  computed: {
    publishedBooksMessage() {
      return this.author.books.length > 0 ? 'Yes' : 'No'
    }
  },
  methods: {
    greet(event) {
      // `this` inside methods points to the current active instance
      alert(`Hello ${this.name}!`)
      // `event` is the native DOM event
      if (event) {
        alert(event.target.tagName)
      }
    },
    async getAnswer() {
      this.answer = 'Am Denken...'
      try {
        const res = await fetch('https://yesno.wtf/api')
        this.answer = (await res.json()).answer
      } catch (error) {
        this.answer = 'Error! Konnte nicht die API erreichen. ' + error
      }
    }
  },
  watch: {
    // Immer wenn die Frage sich ändert, wird diese Funktion ausgeführt
    question(newQuestion) {
      if (newQuestion.indexOf('?') > -1) {
        this.getAnswer()
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
