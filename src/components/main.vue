<template>
<main>
    <h1>main</h1>
</main>
</template>


<script>
export default{
    name: 'AppMain',
    data(){
        return{
            moviesList: []
        }
    },
    created(){
        axios.get('https://api.coindesk.com/v1/bpi/currentprice.json').then((res)=>{
            this.moviesList = res.data.response
        })
    }
}
</script>

<style scoped lang="scss">
</style>
