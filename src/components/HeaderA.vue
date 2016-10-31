<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <h2>{{ msgfromfather }}</h2>
    <button @click="onClickMe">Click</button>
    <button @click="openMouse">openMouse</button>
    <button @click="openDispath">openDispath</button>
  </div>
</template>

<script>
  export default {
    data () {
      return {
        // note: changing this line won't causes changes
        // with hot-reload because the reloaded component
        // preserves its current state and we are modifying
        // its initial state.
        msg: 'in HeaderA '
      }
    },
    props: ['msgfromfather'],
    events:{
      'onAddnew':function (items) {
        console.log(items);
      }
    },
    methods: {
      onClickMe: function () {
        console.log(this.msgfromfather);
      },
      openMouse: function () {
        this.$emit("child-tell-me-something", this.msg)
      },
      openDispath:function () {
        this.$dispatch("child-tell-me-dispath", this.msg)
      }
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  h1 {
    color: #42b983;
  }
</style>
