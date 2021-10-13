<template>
    <div class="post max-w-screen-xl mr-auto ml-auto">
        <search @updateResult="updateSearch"></search>
        <posts :resultSearch="resultSearch"></posts>
    </div>
</template>

<script>
import posts from "../components/posts.vue"
import search from "../components/search.vue"
export default {
    name: "home",
    data(){
        return{
            resultSearch:[]
        }
    },
    components:{
        posts,
        search,
    },
    methods:{
        updateSearch(key){
           this.resultSearch=key
            // console.log(process.env.VUE_APP_LINK_SEARCH+key1+"&apiKey="+process.env.VUE_APP_API_KEY)
        },
    },
    // mounted(){
       
    // }
}
</script>

<style>

</style>