<template>
  <div id="app">
    <header>
      <h1>My Music</h1>
    </header>
    <main>
      <section class='player'>
        <h2 class='song-title'>{{current.title}}</h2>
        <!-- data에서 가져옴. props. data. (state) 사용가능 -->
      </section>
    </main>
  </div>
</template>

<script>


export default {
  name: 'App',
  data: function(){
    return{
     current:{
       title: 'SONG TITLE'
     },
     songs: [
       {title: 'Song1', artist: 'Kim', src: require('')},
       {title: 'song2', artist: 'Kim', src: require('')},
       {title: 'Song3', artist: 'Kim', src: require('')}
       //src 가져올 때 그냥 가져올 수 없음. require 필요. 이미지. mp3같은 파일들은 src > asset에 저장 후 사용한다
     ]
    }
  }
  // data : react 의 state역할 함
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
