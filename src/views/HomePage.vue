<template>
  <div id="app">
    <div class="container">
      <div class="card-list">
        <CardItem v-for="news in newsList.results" :key="news.id"
          :cardTitle="news.title"
          :cardContent="news.overview"
          :cardImage="news.poster_path"
          :cardDate="news.release_date"
          :cardID="news.id"
          :cardRating="news.vote_average"
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
      newsList: []
    }
  },
  methods : {
    fetchNews() {
      fetch('https://api.themoviedb.org/3/movie/popular?api_key=0a81e077e4c0f82efa0825b92e9ecee6&language=en-US&page=1')
      .then(response => response.json())
      .then(data => {
        this.newsList = data;
        console.log(this.newsList);
      })
    }
  },
  mounted() {
    this.fetchNews();
  }
}
</script>

<style scoped>
body {
	background: #7bcdea;
	
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
@media(min-width: 768px)and(max-width: 1024px){
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
