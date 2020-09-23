<template>
  <div>
    <input type="text" v-model="textSearch " />
    <button @click="search()">Search</button>
 <b-card-group columns>
      <b-card
        v-for="movie in movieList"
        :key="movie.id"
        :title="movie.title"
        img-top
        tag="article"
        style="max-width: 20rem;"
        class="mb-2"
      >
      <b-card-text class="alert alert-info text-truncate">
           Overview:{{movie.overview}} 
        
        </b-card-text>
        <b-card-text class="alert alert-warning">
           Score {{movie.vote_average}} <br>
          Release Date {{ movie.release_date}}
        </b-card-text>
        <b-button href="#" variant="warning">Detail</b-button>
      </b-card>
    </b-card-group>



  </div>
</template>

<script>
import axios from 'axios';
export default {
    data(){
        return{
            movieList:null,
             textSearch: "",

        };

    },
   methods: {
     search(){
      axios.get("https://api.themoviedb.org/3/search/movie?api_key=ea1e4e94cd0464ac689ddcc8affadfb6&query=+"+this.textSearch)
      
      .then((Response) => {
        this.movieList = Response.data.results;
        console.log(this.movieList);
      }) 
      .catch((err) => {
        console.log(err)
      })
    },
    
    }
    }
</script>

<style>

</style>