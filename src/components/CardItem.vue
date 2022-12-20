<template>
  <div class="card">
  <router-link :to="'/single-news/'+ cardID" >
  <div class="card-image">
    <figure class="image is-4by3">
      <img :src="'https://image.tmdb.org/t/p/original'+cardImage" :alt="cardTitle">
    </figure>
  </div>
  <div class="card-content">
    <div class="media">
      <div class="media-content">
        <p class="title is-4">{{cardTitle}}</p>
        <time datetime="2016-1-1">{{cardDate}}</time>
      </div>
    </div>

    <div class="content">
      <div v-html="cardContent"></div>
      
    </div>
    <div class="rating">
      <p class="title is-6">Rating: {{cardRating}}</p>
      
    </div>
  </div>
</router-link>
</div>
</template>

<script>
export default {
  name: 'CardItem',
  props: {
    cardTitle: String,
    cardContent: String,
    cardImage: String,
    cardDate: String,
    cardID: Number,
    cardRating:Number
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
