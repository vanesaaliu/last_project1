<template>
  <article class="single-article">
    <div class="container">
      <div class="single-Movie"></div>
      <div class="single-article__image">
        <img :src="'https://image.tmdb.org/t/p/original'+articleImage" :alt="articleImage">
      </div>
      <div class="single-movie">
      <div class="single-article__content content">
        <div > {{ articleContent }}</div>
      </div>
      <div class="viti">
        <div> Release Year: {{ articleDate }}</div>
      </div>
      <div class="rating">
        <div>Rating: {{ articleRating }}</div>
      </div>
    </div>
      
    </div>
  </article>

</template>

<script>
export default {
  name: 'SingleNews',
  data() {
    return {
      articleContent: '',
      articleImage: '',
      articleRating:''
    }
  },
  methods: {
    fetchSingleNews(newsID) {
      fetch('https://api.themoviedb.org/3/movie/'+ newsID+'?api_key=0a81e077e4c0f82efa0825b92e9ecee6&language=en-US&page=1')
      .then(response => response.json())
      .then(data => {
        console.log(data);
        this.articleContent = data.overview;
        this.articleImage = data.poster_path;
        this.articleRating=data.vote_average;
        this.articleDate=data.release_date;
      })
    }
  },
  mounted() {
    this.fetchSingleNews(this.$route.params.id);
  }
}
</script>

<style>
.single-article {
  padding-top: 60px;
  padding-bottom: 60px;
  text-align: left;
}
.column{
  display: flex;
  align-items: center;
  justify-content: flex-start;
  flex-direction: row;
  flex-wrap: wrap;
 
}
.single-article__image{
  display: flex;
  justify-content: space-around;
  
}
.rateLogo{
  width: 15px;
  height: 15px;
}
img {
    width: 60%;
    height: 20%;
  }
</style>