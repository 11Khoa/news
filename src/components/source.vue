<template>
  <div class="source">
      <ul>
          <li @click="select(item)" :class="{'active': nameSource==item.toLowerCase()}" class="text-left cursor-pointer md:hover:text-red-500 <sm:text-center" v-for="item in source" :key="item.id">{{item}}</li>
      </ul>
  </div>
</template>

<script>
export default {
    props:["source"],
    data(){
        return {
            nameSource:"all",
            selected:false
        }
    },
    methods:{
        select(name){
            this.nameSource=name.toLowerCase()
            this.$emit('name-news', name)
        }
    }
}
</script>

<style>
.source li.active{
    color: red;
}
</style>