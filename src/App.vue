<template>
  <div>
    <div class="playerInputs">
      42245681
      220612
      <input type="text" value="42245681"  ref="player1">
      <input type="text"  value="220612"  ref="player2">
      <button v-on:click="getPlayers">GO!</button>
    </div>

    <div class="leftPlayer" v-if="player1">
      {{ player1.profile.personaname }}
      <img src:player1.profile.avatar alt="">
      {{ player1.solo_competitive_rank }}
    </div>
    <div class="rightPlayer" v-if="player1">
      {{ player2.profile.personaname }}
      <img src:player2.profile.avatar alt="">
      {{ player2.solo_competitive_rank }}
    </div>

    <div class="rightPlayer">

    </div>
  
    <ul v-if="errors && errors.length">
      <li v-for="error of errors">
        {{error.message}}
      </li>
    </ul>
  </div>
</template>

<style>
.leftPlayer {
  width:40%;
  float: left;
}

.rightPlayer {
  float:right;
  width: 40%;
}
</style>


<script>
import axios from 'axios';

export default {
  data() {
    return {
      player1: '',
      player2: '',
      posts: '',
      errors: ''
    }
   
  },
   methods: {
    getPlayers: function (event) {
      // setting urls from inputs
      var player1Url = 'https://api.opendota.com/api/players/' + this.$refs.player1.value; 
      var player2Url = 'https://api.opendota.com/api/players/' + this.$refs.player2.value;
     
     // getting data from api, probably a cleaner way to do this
      axios.get(player1Url)
      .then(response => {
        // JSON responses are automatically parsed.
        this.player1 = response.data
      })
      .catch(e => {
        this.errors.push(e)
      })
       axios.get(player2Url)
      .then(response => {
        // JSON responses are automatically parsed.
        this.player2 = response.data
      })
      .catch(e => {
        this.errors.push(e)
      })
    }
  },
}
</script>