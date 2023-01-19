<template>
  <div class="movies">
     <div class="movies__box" v-for="movie in listOfMovies" :key="movie">
       <div class="info">
         <div class="info__title">
           <span>{{ movie.movieTitle }}</span>
           <span>{{ movie.movieFullTime }} minuty</span>
         </div>
         <button class="info__play" @click="() => open(movie.id)">
           <img src="@/assets/play.png" style="width:20px;" alt="Play button"/>
           <span>Obejrzyj film</span>
         </button>
       </div>
       <div v-if="movie.isOpen" class="movie">
           <video @play="start" @pause="middle" @ended="end" controls>
             <source :src="movie.movieUrl" type="video/mp4">
           </video>
       </div>
     </div>
  </div>
</template>

<script>
import {reactive} from "vue";
import movie1 from "@/assets/movies/movie1.mp4"
import movie2 from "@/assets/movies/movie2.mp4"
import movie3 from "@/assets/movies/movie3.mp4"
import movie4 from "@/assets/movies/movie4.mp4"
export default {
  name: 'MoviesList',
  components:{},
  setup(){
    const movies = reactive([
      movie1, movie2, movie3, movie4
    ])
    const listOfMovies = reactive([
      {
        id:0,
        movieTitle:'W pustyni i w puszczy',
        movieUrl:'',
        movieFullTime:null,
        isOpen:false
      },
      {
        id:1,
        movieTitle:'Tajemniczy smark na firanie',
        movieUrl:'',
        movieFullTime:null,
        isOpen:false
      },
      {
        id:2,
        movieTitle:'Zabójcza opona',
        movieUrl:'',
        movieFullTime:null,
        isOpen:false
      },
      {
        id:3,
        movieTitle:'Czeski film',
        movieUrl:'',
        movieFullTime:null,
        isOpen:false
      }
    ]);

    listOfMovies.map((item,index) => item.movieUrl = movies[index])

    function open(index) {
      const currentMovie = listOfMovies.find(movie => movie.id === index);
      if(currentMovie.isOpen) {
        currentMovie.isOpen = false;
        return;
      }
      listOfMovies.forEach((movie, i) => {
        movie.isOpen = i === index;
      });
    }
    return{
      listOfMovies,
      open,movies
    }
  },
  mounted() {
    if (Array.isArray(this.$refs.video) && this.$refs.video.length > 0) {
      this.$refs.video.forEach(video => {
        video.addEventListener('play', this.start)
        video.addEventListener('pause', this.middle)
        video.addEventListener('ended', this.end)
      })
    }
  },
  methods: {
    start() {
      console.log('początek filmu')
    },
    middle() {
      console.log('środek filmu')
    },
    end() {
      console.log('koniec filmu')
    }
  }
}
</script>


<style scoped lang="scss">

.movies {
  display:flex;
  align-items: center;
  justify-contect:center;
  flex-direction: column;
  padding:0 1em;
  width:100%;
  &__box {
    display:flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;
    margin-bottom:2em;
    width:100%;
    height:100%;
    background: rgba(196, 196, 196, 0.01);
    box-shadow: inset 0px 39px 56px -36px rgba(255, 255, 255, 0.1), inset 0px 7px 11px -4px #FFFFFF, inset 0px -82px 68px -64px rgba(96, 68, 145, 0.1), inset 0px 98px 100px -48px rgba(202, 172, 255, 0.1), inset 0px 4px 18px rgba(154, 146, 210, 0.1), inset 0px 1px 40px rgba(227, 222, 255, 0.2);
    backdrop-filter: blur(50px);
    border-radius: 120px;
  }
  .info {
    display:flex;
    align-items: center;
    justify-content: space-between;
    padding:2em;
    width:80%;
    &__title {
      display:flex;
      align-items:start;
      justify-content: center;
      flex-direction: column;
      :nth-child(1){
        margin-bottom:.4em;
        font-size:1.3rem;
      }
      :nth-child(2){
        font-size:.8rem;
      }
    }
    &__play {
      display:flex ;
      align-items: center;
      justify-content: center;
      flex-direction: column;
      background-color:transparent;
      border:none;
      cursor:pointer;
      span {
        margin-top:.4em;
        color:white;
      }
    }
   }
  .movie, video {
    width:100%;
    height:100%;
  }
}
</style>
