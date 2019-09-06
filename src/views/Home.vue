<template>
  <div class="home centered">
    <div class="input -group input-div">
      <h4 style="color:white">Search for a name </h4>
    <input class="text" type="text" v-model="searchVoice" value="" />
    </div>
    <button type="button" @click="getVoice123Actors(searchVoice)" > Search </button>
    
  <ul v-for="user in Users" :key="user.id">
    <li><a style="color:white" v-bind:href="`https://voice123.com/${user.user.username}`"><h2>{{user.user.username}}</h2></a></li>
    <li> <img src="../assets/download.png" alt="Avatar" /></li>
    <li> <audio controls>
          <source v-bind:src="`{user.relevant_sample.file}`" type="audio/mpeg">
            Your browser
            </audio>
     </li>
  </ul>
  
  <div>
    <button @click="prevPage">
    Previous
  </button>
  &nbsp;
   &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;
  <button @click="nextPage">
    Next
  </button>
  </div>
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
      Users: [],
      pageNumber: 0
    }
  },
  props:{
    listData:{
      type:Array,
      required:true
    },
    size:{
      type:Number,
      required:false,
      default: 10
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
     
    },
    nextPage(){
         this.pageNumber++;
      },
      prevPage(){
        this.pageNumber--;
      }
  },
  computed: {
    paginatedData(){
    const start = this.pageNumber * this.size,
          end = start + this.size;
     return this.listData.slice(start, end);
}
  },
  components: {
  }
};
</script>

<style lang="scss" scoped>

.centered{
    position: fixed;
  top: 30%;
  left: 25%;
}
.input-div{
  display: inline;

}
.text{
  width: 600px;
  height: 50px;
  margin-bottom: 30px;
}
button{
  width: 150px;
  height: 50px;
  margin-bottom: 30px;
}
</style>

