<template>
    <div id="app">
      <div class="container">
        <div class="movie-filters">
        <div class="year-filter"><h3>Year</h3><input type="text" v-model="year" class="input is-focused" placeholder="Search by year"></div>
        <div class="rating-filter"><h3>Rating</h3><input type="text" v-model="rating" class="input is-focused"></div>
        <button class="button is-link is-outlined" @click="fetchNews()">Search</button>
        </div>
        <div class="card-list">
          <CardItem v-for="news in newsList.results" :key="news.id"
            :cardTitle="news.title"
            :cardContent="news.overview"
            :cardImage="news.poster_path"
            :cardDate="news.release_date"
            :cardID="news.id"
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
        newsList: [],
        year:" ",
        rating:""
      }
    },
    methods : {
      fetchNews() {
        fetch('https://api.themoviedb.org/3/discover/movie?api_key=0a81e077e4c0f82efa0825b92e9ecee6&language=en-US&primary_release_year='+this.year+'&vote_average.gte='+this.rating+'&vote_average.lte='+this.rating+'&sort_by=vote_average.desc&page=1')
        .then(response => response.json())
        .then(data => {
          this.newsList = data;
          console.log(this.newsList);
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
    color: #485fc7;
  }
    .card-list {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 30px;
      padding-top: 60px;
      padding-bottom: 60px;
    }
    img {
      object-fit:  cover !important;
    }
  </style>
  