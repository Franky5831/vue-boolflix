<template>
<main>
    <input v-model="searchText" placeholder="cerca"> 
    <button @click="search(searchText)">vai</button>
    <ul>
        <h1 v-show="this.showRes">Films</h1>
        <li v-for="film in movies" :key="film.id">
        film: {{film.title}}
        </li>
    </ul>
    <ul>
        <h1 v-show="this.showRes">Serie TV</h1>
        <li v-for="tv in series" :key="tv.id">
        serie: {{tv.original_name}}
        </li>
    </ul>
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
            showRes: false,
            searchText: '',
        }
    },
    methods:{
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
main{
    margin: 20px 50px;
}
</style>
