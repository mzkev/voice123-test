<template>
  <div class="home centered">
    <input type="text" v-model="searchVoice" value="" />
    <button type="button" @click="getVoice123Actors(searchVoice)" > Search </button>
    
  <ul v-for="user in Users" :key="user.id">
    <li><a href="https://voice123.com/" >{{user.user.username}}</a></li>
    <li> <img src="../assets/download.png" alt="Avatar" /></li>
   
  </ul>
  </div>
</template>

<script>
// @ is an alias to /src

export default {
  name: "home",
  data() {
    return {
      searchVoice: "",
      VoiceActors: [],
      Users: []
    }
  },
  methods: {
    getVoice123Actors: async function(searchVoice){
      const res = await fetch(" https://api.sandbox.voice123.com/providers/search/?service=voice_over&keywords=search%20text&page=",{
        method: "GET"
      }).then(result => result.json());
      this.VoiceActors = res.providers;
      console.log(this.VoiceActors);
    this.Users = this.VoiceActors.filter(actor => actor.user.username.toLowerCase().startsWith(searchVoice.toLowerCase()));
     
    }
  },
  components: {
  }
};
</script>

<style lang="scss" scoped>

.centered{
    position: fixed;
  top: 50%;
  left: 50%;
  margin-top: -50px;
  margin-left: -100px;
}
</style>

