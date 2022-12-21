<template>
  <div class="card">
  <router-link :to="'/single-news/'+ movieID" >
    <div class="card">
  <div class="card-image">
    <figure class="image is-4by3">
      <img :src="'https://image.tmdb.org/t/p/original'+movieImage" :alt="movieTitle">
    </figure>
  </div>
  <div class="card-content">
    <div class="media">
      <div class="media-content">
        <p class="title is-4">{{movieTitle}}</p>
        <time datetime="2016-1-1">{{movieDate}}</time>
      </div>
    </div>

    <div class="content">
      <div><p class="content-paragraph">{{ movieContent }}</p></div>
      
    </div>
    <div class="rating">
      <p class="title is-6">Rating: {{movieRating}}</p>
    </div>
    </div>
  </div>
</router-link>
</div>
</template>

<script>
export default {
  name: 'CardItem',
  props: {
    movieTitle: String,
    movieContent: String,
    movieImage: String,
    movieDate: String,
    movieID: Number,
    movieRating:Number
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.card:hover {
  background-color: rgb(0, 140, 159);
}
.content-paragraph{
  display: -webkit-box;
  -webkit-line-clamp: 3;
  -webkit-box-orient: vertical;
  overflow: hidden;
  font-size: 16px;
}

@media(max-width:767px){
  
  .card-content{
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
  max-width: 200px;
}
@media(min-width: 768px)and(max-width: 1024px){

}
}

</style>
