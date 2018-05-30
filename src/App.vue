<template>
  <div id="app">
    <img src="./assets/logo.png">
    <h1>{{ msg }}</h1>
    <h2>Players</h2>
    <div class="container">
      <ul class="playerlist" v-if="posts && posts.length">
        <li v-for="player in this.posts" v-bind:class="{active:isActive===player.id}" v-bind:key="player.id" @click="playerData(player.id)">
          {{player.name}}
        </li>
      </ul>
      <div class="playerdata">
        <div class="player"  v-if="playerStatistics.data && playerStatistics.data.length">
          <b>Name:</b> {{playerStatistics.data[0].name}}<br>
          <b>Ranking:</b> {{playerStatistics.data[0].ranking}}<br>
          <b>Klubb:</b> {{playerStatistics.data[0].teamName}}<br>
          <b>Liga:</b> {{playerStatistics.data[0].tournamentName}}<br>
          <b>Ålder:</b> {{playerStatistics.data[0].age}}<br>
          <b>Vikt:</b> {{playerStatistics.data[0].weight}}<br>
          <b>Längd:</b> {{playerStatistics.data[0].height}}<br>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  import axios from 'axios'
  export default {
    name: 'app',
    methods: {
      playerData: function (id) {
        this.isActive = id;
        axios.get(`//localhost:3000/api/player/${id}`)
          .then(response => {
            this.playerStatistics = response;
          })
          .catch(e => {
            alert(`Error reading player data from server!`);
            // this.errors.push(e)
          })
      },
      populate: function() {
        alert(JSON.stringify(this.posts));
      }
    },
   data () {
    return {
      msg: 'Soccer statistics',
      // posts: {id:'',name:''}
      posts: {},
      playerStatistics: {},
      isActive: '',
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
        alert('Error reading players from server! Perhaps server not started?');
        // this.errors.push(e)
      })
  }
}
</script>

<style lang="scss">
  .container {
    display: flex;
  }
  .playerdata {
    width: 300px;
    margin: 0 auto;
  }
  .player {
    text-align: left;
  }
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
        font-weight: 600;
        color: green;
      }
      &.active {
        color: green;
        text-decoration: underline;
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
