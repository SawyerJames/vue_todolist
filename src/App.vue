<template>
  <div id="app">
    <hello></hello>
    <h1>{{ title }}</h1>
    <input v-model="newItem" @keyup.enter="addNew"></input>
    <ul>
      <li v-for="item in items" v-bind:class="{finished: item.isFinished}" v-on:click="toggleFinish(item)">
        {{ item.lable }}
      </li>
    </ul>
  </div>
</template>

<script>
import Store from './store.js'
import Hello from './components/Hello.vue'
export default {
  data: function () {
    return {
      title: 'Your Todo List',
      items: Store.fetch(),
      newItem: ''
    }
  },
  components: {
    Hello
  },
  methods: {
    toggleFinish: function (item) {
      item.isFinished = !item.isFinished
    },
    addNew: function () {
      this.items.push({
        lable: this.newItem,
        isFinished: false
      })
      this.newItem = ''
    }
  },
  watch: {
    items: {
      handler: function (items) {
        Store.save(items)
      },
      deep: true
    }
  }
}
</script>

<style>
.finished{
  text-decoration:underline;
}

html {
  height: 100%;
}

body {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100%;
}

#app {
  color: #2c3e50;
  margin-top: -100px;
  max-width: 600px;
  font-family: Source Sans Pro, Helvetica, sans-serif;
  text-align: center;
}

#app a {
  color: #42b983;
  text-decoration: none;
}

.logo {
  width: 100px;
  height: 100px
}
</style>
