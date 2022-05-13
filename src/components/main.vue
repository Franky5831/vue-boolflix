<template>
<main>
    <div id="search">
        <input @keydown.enter="search(searchText)" v-model="searchText" placeholder="cerca"> 
        <button @click="search(searchText)">vai</button>
    </div>
    <div id="resoultsSearch">
        <h1 v-show="this.showRes">Films</h1>


        <swiper :slides-per-view="4" :loop="false" @swiper="onSwiper" @slideChange="onSlideChange">
            <swiper-slide v-for="film in movies" :key="film.id" @mouseover="hover = true" @mouseleave="hover = false">
                <div class="card" v-bind:style="{ 'background-image': 'url(' + 'https://image.tmdb.org/t/p/w342/'+  film.poster_path + ')' }">
                    <h1 v-if="hover">{{film.title}}</h1>
                </div>
            </swiper-slide>
        </swiper>

        <h1 v-show="this.showRes">Serie TV</h1>
        <swiper :slides-per-view="4" :loop="false" @swiper="onSwiper" @slideChange="onSlideChange">
            <swiper-slide v-for="tv in series" :key="tv.id">
                <div blank="true" class="card test img-fluid w-100 mx-auto" :class="{test_2: true}" >
                    <img src='https://img.animeworld.tv/locandine/uvprg.jpg'>
                </div>
            </swiper-slide>
        </swiper>
    </div>





        <swiper
      :slides-per-view="3"
      :space-between="30"
      :loop="true"
      @swiper="onSwiper"
      @slideChange="onSlideChange"
    >
      <swiper-slide
        v-for="(tv, index) in series"
        :key="index"
        class="test"
        :class="{test_2: true}"
      >
        <img
          src="https://i.picsum.photos/id/32/600/400.jpg?hmac=nmoK32Lpfqcg85iHyNxf1t1fD69dL4HMZN0I3KBAsOo"
          width="600"
          height="400"
          class="img-fluid w-100 mx-auto"
          blank="true"
        >
      </swiper-slide>
    </swiper>









</main>
</template>


<script>
import axios from 'axios';

import { Navigation, Pagination } from 'swiper'
import { SwiperCore, Swiper, SwiperSlide } from 'swiper-vue2'
import 'swiper/swiper-bundle.css'

SwiperCore.use([Navigation, Pagination])


export default{
    components: {
        Swiper,
        SwiperSlide
    },


    name: 'AppMain',
    data(){
        return{
            movies: [],
            series: [],
            apiKey: '9c08889b4156aa846587f4aff22355b6',
            apiPath: 'https://api.themoviedb.org/3/search/',
            showRes: false,
            searchText: '',
            hover: false
        }
    },
    methods:{
        getImageUrl (imageId) {
            return `https://picsum.photos/600/400/?image=${imageId}`
        },
        onSwiper (swiper) {
            console.log(swiper)
        },
        onSlideChange () {
            console.log('slide change')
        },


        search(text){
            const queryData = {
                params:{
                    api_key: this.apiKey,
                    query: text
                }
            }
            this.getMovies(queryData);
            this.getSeries(queryData);
            this.showRes = true;
            console.log(this.showRes)
        },
        getMovies(queryData){
            axios.get(this.apiPath+'movie', queryData).then((ris)=>{
                this.movies = ris.data.results;
            }).catch((err)=>{
                console.log(err);
            })
        },
        getSeries(queryData){
            axios.get(this.apiPath+'tv', queryData).then((ris)=>{
                this.series = ris.data.results;
            }).catch((err)=>{
                console.log(err);
            })
        }
    }
}
</script>

<style scoped lang="scss">
.img-fluid {
  max-width: 100%;
  height: auto;
}
.w-100 {
  width: 100%;
}
.ml-auto, .mx-auto {
  margin-left: auto;
}
.mr-auto, .mx-auto {
  margin-right: auto;
}






.swiper-slide{
    width: 350px;
    margin: 20px;
}

main{
    margin: 20px 50px;

    #search{
        display: flex;
        height: 40px;
        
        input{
            width: calc(100% - 70px);
            height: 100%;
            font-size: 30px;
            padding-left: 20px;
        }
        button{
            font-size: 30px;
            width: 70px;
            height: 100%;
        }
    }
    #resoultsSearch{
        display: flex;
        flex-direction: column;
            .card{
                width: 350px;
                height: 500px;
                background-repeat: no-repeat;
                background-size: cover;
                display: flex;
                flex-direction: column;
                justify-content: flex-end;
                h1 {
                    text-align: end;
                      vertical-align: text-bottom;
                    width: 100%;
                    font-size: 25px;
                    -webkit-text-stroke: 1px black;
                    color: white;
                    text-shadow: 0px 0px #000,
                }
            }
    }
}
</style>
