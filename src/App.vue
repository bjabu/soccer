<template>
  <div id="app">
    <img src="./assets/logo.png">
    <h1>{{ msg }}</h1>
    <h2>Players</h2>
    <ul class="playerlist" v-if="posts && posts.length">
      <li v-for="player in this.posts" v-bind:key="player.id" @click="populate(player.id)">
        {{player.name}}
      </li>
    </ul>
  </div>
</template>

<script>
  import axios from 'axios'
  export default {
   name: 'app',
    methods: {
      populate: function() {
        alert(JSON.stringify(this.posts));
      }
    },
   data () {
    return {
      msg: 'Soccer statistics',
      // posts: {id:'',name:''}
      posts: {},
      errors: ''
    }
   },
  created() {
    axios.get('//localhost:3000/api/players')
      .then(response => {
        // JSON responses are automatically parsed.
        this.posts = response.data
      })
      .catch(e => {
        this.errors.push(e)
      })

    // async / await version (created() becomes async created())
    //
    // try {
    //   const response = await axios.get(`http://jsonplaceholder.typicode.com/posts`)
    //   this.posts = response.data
    // } catch (e) {
    //   this.errors.push(e)
    // }
  }
}
</script>

<style lang="scss">
  ul.playerlist {
    border: 1px solid darkgrey;
    width: 200px;
    height: 200px;
    margin: 0 auto;
    overflow-y: auto;
    >li {
      line-height: 1.5;
      cursor:pointer;
      &:hover {
        color: blue;
        font-weight: 600;
      }
    }
  }
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  /*display: inline-block;*/
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
