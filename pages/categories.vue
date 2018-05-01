<template>
  <div>
      <ul>
          <li v-for="(item,i) in info" :key="i">
               <nuxt-link :to="{name:'categorie-id',params:{id:info[i].id}}" >{{ info[i].name }}</nuxt-link>
          </li>
      </ul>
  </div>
</template>

<script>
import axios from 'axios'
export default {
    head(){
        return {
            title:'文章分类'
        }
    },
    async asyncData(){
        let {data} = await axios.get('http://www.likecn.cn/wp-json/wp/v2/categories')
        console.log(data);
        return { info:data }
    }
}
</script>