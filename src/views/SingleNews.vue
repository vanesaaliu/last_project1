<template>
  <article class="single-article">
    <div class="container">
      
      <div class="single-article__image">
        <img :src="'https://image.tmdb.org/t/p/original'+articleImage" :alt="articleImage">
      <div class="column is-7" style="padding-bottom: 128px;font-size: 18px;">
      <div class="movie-title"><p class="title is-1 is-spaced">{{ articleTitle }}</p></div>
      <div class="single-article__content content">
        <div > {{ articleContent }}</div>
      </div>
      <div class="year-rating">
      <div class="viti">
        <div> Release Year: {{ articleDate }}</div>
      </div>
      <div class="rating">
        <div>Rating: {{ articleRating }}</div>
    
    </div>
  </div>
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
      articleRating:'',
      articleTitle:''
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
        this.articleTitle=data.title;
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
.content{
  font-size: 25px;
}

.year-rating{
  display: flex;
  flex-direction: column;

}
img {
    width: 40%;
    height: 20%;
}
.title.is-1{
  padding-bottom: 33px;
}
@media(max-width:767px){
  .title.is-1 {
    font-size: 38px;
}
  .year-rating{
  display: flex;
  flex-direction: column;
  font-size: 13px;
}
img{
    width: 51%;
    height: 14%;
    padding-top: 82px;
    }
    .content{
  font-size: 25px;
}
    .single-article__content{
      
  font-size: 15px;
}
.single-article {
  padding-top: 60px;
  padding-bottom: 60px;
  text-align: left;
  display: flex;
  align-items: center;
  justify-content: flex-start;
  flex-direction: row;
  flex-wrap: wrap;
}}
</style>