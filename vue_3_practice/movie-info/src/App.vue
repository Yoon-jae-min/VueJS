<template>
  <Navbar/>
  <Event :text="text[eventTextNum]"/>
  <SearchBar :data="data_tmp" @searchMovie="searchMovie($event)"/>
  <p>
    <button @click="showAllMovie">전체보기</button>
  </p>
  <Movies :data="data_tmp" @openModal="modalFlag=true; selectedMovie=$event" @increaseLike="increaseLike($event)"/>
  <Modal :data="data" :modalFlag="modalFlag" :selectedMovie="selectedMovie" @closeModal="modalFlag = false"/>
</template>

<script>
  import data from './assets/movies';
  import Navbar from './components/Navbar.vue';
  import Event from './components/Event.vue';
  import Modal from './components/Modal.vue';
  import Movies from './components/Movies.vue';
  import SearchBar from './components/SearchBar.vue';
  export default {
    name: 'App',
    data() {
      return{
        modalFlag: false,
        data: data,
        data_tmp: [...data],
        selectedMovie: 0,
        text: ["NEPLIX 강렬한 운명의 드라마, 경기크리쳐", "디즈니 100주년 기념작, 위시", "그날, 대한민국의 운명이 바뀌었다, 서울의 봄"],
        eventTextNum: 0,
        interval: null
      }
    },
    methods:{
      increaseLike(id) {
        this.data.find(movie => {
          if(movie.id == id){
            movie.like += 1;
          }
        })
      },
      searchMovie(title){
        this.data_tmp = this.data.filter(movie => {
          return movie.title.includes(title);
        })
      },
      showAllMovie(){
        this.data_tmp = [...this.data];
      }
    },
    components:{
      Navbar: Navbar,
      Event: Event,
      Modal: Modal,
      Movies: Movies,
      SearchBar: SearchBar
    },
    mounted(){
      this.interval = setInterval(() => {
          this.eventTextNum += 1;
          if(this.eventTextNum === this.text.length){
            this.eventTextNum = 0
          }
        }, 3000);
    },
    unmounted(){
      clearInterval(this.interval);
    }
  }
</script>

<style>
  *{
    box-sizing: border-box;
    margin: 0;
  }
  body{
    max-width: 768px;
    margin: 0 auto;
    padding: 20px;
  }
  h1, h2, h3{
    margin-bottom: 1rem;
  }
  p{
    margin-bottom: 0.5rem;
  }
  button{
    margin-right: 10px;
    margin-top: 1rem;
  }
  .item{
    width: 100%;
    border: 1px solid #ccc;
    display: flex;
    margin-bottom: 20px;
    padding: 1rem;
  }
  .item figure{
    width: 30%;
    margin-right: 1rem;
  }
  .item img{
    width:100%;
  }
  .item .info{
    width: 100%;
  }
  .modal{
    background-color: rgba(0, 0, 0, 0.7);
    position: fixed;
    left: 0;
    top: 0;
    width: 100%;
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
  }
  .modal .inner{
    background-color: #fff;
    width: 80%;
    padding: 20px;
    border-radius: 10px;
  }
</style>
