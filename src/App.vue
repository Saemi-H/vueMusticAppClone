<template>
  <div id="app">
    <header>
      <h1>My Music</h1>
    </header>
    <main>
      <section class='player'>
        <h2 class='song-title'>{{current.title}} - <span>{{current.artist}}</span></h2>
          <!-- data에서 가져옴. props. data. (state) 사용가능 -->
        <!-- <h2 class='song-title'>{{song.title}} - <span>{{song.artist}}</span></h2> -->
      <!-- 에러생김. current 배열에서 데이터 가져와야함 -->
        <div class="controls">
          <button class='prev' @click='prev'>Prev</button>
          <button class='play' v-if='!isPlaying' @click='play'>Play</button>
          <button class='pause' v-else @click='pause'>Pause</button>
          <button class='next' v-if='isPlaying' @click='next'>Next</button>
          <!-- v-if '!' == v-else-->
        </div>
      </section>
      <section class="playlist">
        <h3>The Playlist</h3>
        <button v-for='song in songs' :key='song.id' @click='play(song)' :class='(song.src == current.src ? "song-playing" : "song")'>{{song.title}}-{{song.artist}}</button>
        <!-- v-for 로 map처럼 for loop 돌림 item in array -->
      </section>
    </main>
  </div>
</template>

<script>


export default {
  name: 'App',
   // data : react 의 state역할 함
  data: function(){
    return{
     current:{
      //  title: 'SONG TITLE'
     },
     index:0,
     isPlaying:false,
     songs: [
       {id:0, title: 'Song1', artist: 'Kim'},
       {id:1,title: 'song2', artist: 'Kim'},
       {id:2,title: 'Song3', artist: 'Kim'},
      //  {title: 'Song3', artist: 'Kim', src: require('')},
       //src 가져올 때 그냥 가져올 수 없음. require 필요. 이미지. mp3같은 파일들은 src > asset에 저장 후 사용한다
     ],
     player: new Audio()
    }
  },
  methods:{
    play(song){
      if (typeof song.id !== 'undefined'){
        this.current = song;
        this.player.id=this.current.id
        // this.player.src = this.current.src
      }
      this.player.play();
      this.player.addEventListener('ended', function(){
        this.index++;
        if(this.index > this.songs.length-1){
          this.index=0;
        }
      }.bind(this));
      //()=> arrow function 쓰면 안됨 
      this.isPlaying=true;
       console.log(this.current)
    },
    pause(){
      this.player.pause();
      this.isPlaying=false;
    },
    prev(){
      this.index--;
      if(this.index <= 0){
        this.index =0;
      }
      this.current=this.songs[this.index];
      this.play(this.current)
    },
    next(){
      this.index++;
      if(this.index > this.songs.length-1){
        this.index=0;
      }
      this.current = this.songs[this.index];
      this.play(this.current)
    },
  },
  created(){
    this.current = this.songs[this.index];
    // this.player.src=this.current.src;
    // this.player.play()
   
  }
  
}
</script>

<style>
  *{
    padding: 0;
    margin: 0;
    box-sizing: border-box;
  }
  body{
    font-family: sans-serif;
  }
  header{
    display: flex;
    justify-content: center;
    align-content: center;
    width: 100%;
    padding: 15px;
    background-color: #212121;
    color: #fff;
  }
</style>
