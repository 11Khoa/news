<template>
    <div class="flex justify-between relative z-10 <sm:flex-wrap">
        <div class="categories w-1/4 <sm:w-full <sm:ml-4 <sm:mr-4 <sm:mb-5">
            <sourcenews :source="source_news" @name-news="onfilter"></sourcenews>
        </div>
        <div class="w-3/4 ml-10 <sm:w-full <sm:ml-3 <sm:mr-3">
            <post :posts="Allpost" :update="resultSearch"></post>
        </div>
    </div>
</template>

<script>
import axios from "axios"
import post from "../components/post.vue"
import sourcenews from "../components/source.vue"
export default {
    name: "posts",
    components:{
        post,
        sourcenews
    },
    props:["resultSearch"],
    data(){
        return {
            posts:[],
            source_news:[],
            filters:"All",
            result:[]
        }
    },
    created (){
        axios
        .get(process.env.VUE_APP_LINK+process.env.VUE_APP_API_KEY)
        .then(res =>{
            this.posts=res.data.articles;
            const data =this.posts;
            this.source_news.push("All")
            data.forEach(el => {
                // console.log(this.source_news.indexOf(el.source.name)+"::::"+el.source.name);
                if(this.source_news.indexOf(el.source.name)===-1){
                    this.source_news.push(el.source.name)
                }
            });
        })
        .catch(err=>{
            console.log(err);
        })
    },
    methods:{
        onfilter(name){
            this.filters=name
        }
    },
    computed:{
        Allpost(){
            if(this.filters.toLowerCase()!=='all'){
                const result = this.posts.filter(word => word.source.name.toLowerCase()==this.filters.toLowerCase());

                // console.log(result);
                return result
            }else return this.posts
        },
    }
}
</script>

<style>

</style>