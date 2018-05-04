<template>
  <div>
    
    <ul class="article-list">
      <li v-for="(item,i) in article" :key="i">
        <nuxt-link :to="{name:'article-id',params:{id:article[i].id}}" >
          <h2>{{ article[i].title.rendered }}</h2>
          <p v-html="( article[i].excerpt.rendered )"></p>
        </nuxt-link>
      </li>
    </ul>
    <h2>分类列表</h2>
    <ul>
      <li v-for="(item,i) in categories" :key="i">
        <nuxt-link :to="{name:'categorie-id',params:{id:categories[i].id}}">{{ categories[i].name }}</nuxt-link>
      </li>
    </ul>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  data(){
    return {
      article:[],
      categories:[]
    }
  },
 created(){
   axios.all([
     axios.get('http://www.likecn.cn/wp-json/wp/v2/posts'),
     axios.get('http://www.likecn.cn/wp-json/wp/v2/categories'),
     axios.get('http://www.likecn.cn/wp-json/wp/v2/comments')
   ])
   .then(axios.spread((articleres,categoriesres,commentsres)=>{
    //  console.log(articleres.data);
     console.log(articleres.data)
     if (articleres.status == 200) {
       this.article = articleres.data,
       this.categories = categoriesres.data 
     }
   }))
   .catch((error)=>{})
 }
  
}
</script>
