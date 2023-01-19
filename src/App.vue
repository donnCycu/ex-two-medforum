<template>
  <div class="movie">
    <nav class="movie__nav">
      <a class="logo">
        <span>Awesome</span><br/>
        <span>Movie</span>
      </a>
      <ul>
        <li>Home</li>
        <li>Movies</li>
      </ul>
    </nav>
    <div class="movie__list">
      <h2>Watch your favourite movie!</h2>
      <MoviesList/>
    </div>
  </div>
</template>
<script>
import MoviesList from "@/components/MoviesList";
export default {
  name: 'App',
  components: {
    MoviesList
  }
}
</script>

<style lang="scss">
body {
  margin:0;
  padding:0;
  box-sizing: border-box;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  background-color:purple;
}
.movie {
  background: linear-gradient(180deg, #010113 0%, #0E0E31 100%);
  height:100%;
  width:100vw;
  color: #e1e1e1;
  &__nav {
    display:flex;
    align-items: center;
    justify-content: space-between;
    position:fixed;
    top:0;
    left:0;
    right:0;
    padding:1em 2em;
    margin:0 auto;
    width:80%;
    z-index: 2;
    .logo {
      display: flex;
      align-items:start;
      justify-content: start;
      flex-direction: column;
      font-size:1.3rem;
      line-height: 12px;
      letter-spacing: .15em;
    }
    ul {
      display: flex;
      align-items: center;
      justify-content: center;
      list-style-type: none;
      li {
        margin-right:1em;
        padding:.2em 1em;
        text-decoration: none;
        cursor:pointer;
      }
    }
  }
  &__list {
    display:flex;
    align-items: center;
    justify-contect:center;
    flex-direction: column;
    margin:0 auto;
    padding-top:10em;
    width:60%;
    h2 {
      margin-bottom:4em;
    }
  }
}
</style>
