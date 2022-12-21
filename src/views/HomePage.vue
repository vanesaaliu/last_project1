<template>
  <div id="app">
    <div class="container">
      <div class="card-list">
        <CardItem v-for="movie in movieList.results" :key="movie.id"
          :movieTitle="movie.title"
          :movieContent="movie.overview"
          :movieImage="movie.poster_path"
          :movieDate="movie.release_date"
          :movieID="movie.id"
          :movieRating="movie.vote_average"
        >
        </CardItem>
      </div>
    </div>
  </div>
</template>

<script>
import CardItem from '../components/CardItem.vue';

export default {
  name: 'HomePage',
  components: {
    CardItem
  },
  data() {
    return {
      movieList: []
    }
  },
  methods : {
    
    fetchMovie() {
      fetch('https://api.themoviedb.org/3/movie/popular?api_key=0a81e077e4c0f82efa0825b92e9ecee6&language=en-US&page=1')
      .then(response => response.json())
      .then(data => {
        this.movieList = data;
        console.log(this.movieList);
      })
    }
  },
  mounted() {
    this.fetchMovie();
  }
}
</script>

<style scoped>
body {
	background: #63a6be;
	
}
  .card-list {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 30px;
    padding-top: 60px;
    padding-bottom: 60px;
  }
  
  img {
    object-fit:  cover !important;
  }

  @media(max-width:767px){
    .card-list {
    display: grid;
    grid-template-columns: repeat(1, 1fr);
    gap: 30px;
    padding-top: 60px;
    padding-bottom: 60px;
  }
}
@media (min-width: 768px) and (max-width: 1024px){
    .card-list {
    display: grid;
    grid-template-columns: repeat(2,1fr);
    gap: 30px;
    padding: 30px;
  }
  img {
    width: 48%;
    height: 20%;
}}
</style>
