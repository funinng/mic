/* eslint-disable vue/require-v-for-key */
<template>
  <div class="about">
    <h1>{{name}}</h1>
    <div class="">
 <audio autoplay controls :src="this.songdata.url"></audio>
    </div>
    
    <input type="text" v-model="keywords"   @keyup.enter="fun" />
    <button @click="fun">搜索</button>
  <ul>
    <li v-for="site in songs" :key="site.id">
      <span>{{ site.name }}</span>
      <span @click="song(site.id)">{{site.id }}</span>
    </li>
  </ul>
  


  
  </div>
</template>
<script>
export default {
  data(){
    return{
      name:'',
      keywords:'',
      songs:'',
      id:'',
      songdata:'',
      url:''
    }
  },
  methods:{
    fun(){
      this.axios({
        methods:'get',
        url:'http://150.158.4.157:3002/search',
          params:{keywords:this.keywords}
      }).then(res=>{
        this.songs=res.data.result.songs
        console.log(res.data.result.songs);
        console.log(132);
      })
    },
    song(id){
       this.axios({
        methods:'get',
        url:'http://150.158.4.157:3002/song/url',
          params:{id:id}
      }).then(res=>{
        this.songdata=res.data.data[0]
        console.log( this.songdata);
      })

    },
    gechi(){

    }
  }
}
</script>