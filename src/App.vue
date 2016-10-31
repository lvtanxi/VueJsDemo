<template>
  <div id="app">
    <h1 v-text="title"></h1>
    <h2 v-html="contentMsg"></h2>
    <input v-model="newItem" @keyup.enter="addNew">
    <ul>
      <li v-for="item in items" v-text="item.label" :class="{finished:item.isFinished}"
          @click="toggleFinish(item)"></li>
    </ul>
    <p>child tells me:{{words}}</p>
    <header-a msgfromfather="you die !" v-on:child-tell-me-something="lisxx"></header-a>
  </div>
</template>

<script>
  import Store from './store'
  import HeaderA from './components/HeaderA'

  export default {
    data (){
      return {
        title: "this is a todo list",
        contentMsg: "<span>?</span> this is content",
        items: Store.fetch(),
        newItem: "",
        words:""
      }
    },
    events:{
      "child-tell-me-dispath":function (msg) {
        console.log(msg,">>>>");
      }
    },
    methods: {
      toggleFinish: function (item) {
        item.isFinished = !item.isFinished
      },
      addNew: function () {
        this.items.push({
          label: this.newItem,
          isFinished: false
        })
        this.newItem = ""
        this.$broadcast('onAddnew',this.items)
      },
      lisxx: function (msg) {
        this.words = msg
        console.log(msg);
      }
    },
    components: {HeaderA},
    watch: {
      items: {
        handler: function (vals) {
          Store.save(vals)
        },
        deep: true
      }
    }
  }
</script>

<style>
  .finished {
    text-decoration: underline;
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
