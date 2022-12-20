<template>
  <article class="single-article">
    <div class="container">
      <div class="single-article__image">
        <img :src="'https://image.tmdb.org/t/p/original'+articleImage" :alt="articleImage">
      </div>
      <div class="single-article__content content">
        <div > {{ articleContent }}</div>
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
      articleImage: ''
    }
  },
  methods: {
    fetchSingleNews(newsID) {
      fetch('https://api.themoviedb.org/3/movie/'+ newsID+'?api_key=54106cb9e32f32a2f6c166158a3062d4&language=en-US&page=1')
      .then(response => response.json())
      .then(data => {
        console.log(data);
        this.articleContent = data.overview;
        this.articleImage = data[0].poster_path;
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
</style>