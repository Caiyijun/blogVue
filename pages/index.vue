<template>
  <div>
    <!-- <h2>文章列表</h2>
    <ul>
      <li v-for="(item,i) in info" :key="i">
        <nuxt-link :to="{name:'article-id',params:{id:info[i].id}}" >{{ info[i].id }}</nuxt-link>
      </li>
    </ul> -->
    <h2>分类列表</h2>
    <ul>
      <li v-for="(item,i) in cate" :key="i">
        <nuxt-link :to="{name:'categorie-id',params:{id:cate[i].id}}">{{ cate[i].name }}</nuxt-link>
      </li>
    </ul>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  // async asyncData(){
  //     let [article,categorie]=await Promise.all([
  //       axios.get('http://www.likecn.cn/wp-json/wp/v2/posts'),
  //       axios.get('http://www.likecn.cn/wp-json/wp/v2/categories')
  //     ])
  //     return {
  //       info:article,
  //       cate:categorie
  //       }
  // },
  async asyncData(){
      let {data} = await axios.get('http://www.likecn.cn/wp-json/wp/v2/categories')
      return{cate:data}
  }
  
}
</script>
