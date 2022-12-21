<template>
    <div id="app">
      <div class="container">
        <div class="movie-filters">
        <div class="year-filter"><h3 class="year-content">Year</h3><input type="text" v-model="year" class="input is-primary"></div>
        <div class="rating-filter"><h3>Rating</h3><input type="text" v-model="rating" class="input is-primary"></div>
    
        <button class="button is-info is-inverted" @click="fetchMovie()">Search</button>
        </div>
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
       movieList: [],
        year:" ",
        rating:""
      }
    },
    methods : {
      fetchMovie() {
        fetch('https://api.themoviedb.org/3/discover/movie?api_key=0a81e077e4c0f82efa0825b92e9ecee6&language=en-US&primary_release_year='+this.year+'&vote_average.gte='+this.rating+'&vote_average.lte='+this.rating+'&sort_by=vote_average.desc&page=1')
        .then(response => response.json())
        .then(data => {
          this.movieList = data;
          console.log(this.movieList);
        })
      }
    },
  }
  </script>
  
  <style scoped>
  .movie-filters{
    display: flex;
    align-items: center;
    justify-content: center;
    color: white;
  }
  .year-filter {
    display: flex;
    margin-right: 30px;
  }
  .rating-filter{
    display: flex;
    margin-right: 20px;
  }
  h3{
    padding-right: 15px;
    font-weight: 700;
    font-size: 25px;
    color: white;
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
      .movie-filters{
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;

     }
     .single-article__image {
      padding-bottom: 32px;
     }
    .year-content{
      padding-right: 41px;
     }
     .year-filter {
    display: flex;
    margin-right: 30px;
    margin-bottom: 20px;
  }
  .rating-filter{
    
    margin-bottom: 20px;
  }
  
    .card-list {
    display: grid;
    grid-template-columns: repeat(1, 1fr);
    gap: 30px;
    padding-top: 60px;
    padding-bottom: 60px;
  }}
  @media (min-width: 768px) and (max-width: 1024px){
    .card-list {
    display: grid;
    grid-template-columns: repeat(2,1fr);
    gap: 30px;
    padding: 30px;
  }}
  </style>
  