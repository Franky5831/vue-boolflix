<template>
<main>
    <h1>main</h1>
</main>
</template>


<script>
import axios from 'axios';
export default{
    name: 'AppMain',
    data(){
        return{
            movies: [],
            series: [],
            apiKey: '9c08889b4156aa846587f4aff22355b6',
            apiPath: 'https://api.themoviedb.org/3/search/',
        }
    },
    methods:{
        getmovies(queryData){
            axios.get(this.apiPath,'movie', queryData).then((ris)=>{
                this.movies = ris.data.resoults;
            }).catch((err)=>{
                console.log(err);
            })
        },
        getSeries(queryData){
            axios.get(this.apiPath,'tv', queryData).then((ris)=>{
                this.series = ris.data.resoults;
            }).catch((err)=>{
                console.log(err);
            })
        }
    }
}
</script>

<style scoped lang="scss">
</style>
