<template>
  <div>
    <ul class="article-content">
      <li v-for="(item,i) in article" :key="i" class="article-list">
        <nuxt-link :to="{name:'article-id',params:{id:article[i].id}}" >
          <h2>{{ article[i].title.rendered }}</h2>
          <div class="des" v-html="( article[i].excerpt.rendered )"></div>
        </nuxt-link>
        <span class="time-tip">{{ AllDateList[i] }}</span>
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
      categoriesre:[],
      articleTime:[],
      AllDateList:[]
    }
  },
 created(){
   axios.all([
     axios.get('http://www.likecn.cn/wp-json/wp/v2/posts'),
     axios.get('http://www.likecn.cn/wp-json/wp/v2/categories'),
     axios.get('http://www.likecn.cn/wp-json/wp/v2/comments')
   ])
   .then(axios.spread((articleres,categoriesr,commentsres)=>{
    // console.log(articleres.data)
    console.log(categoriesr.data)
     if (articleres.status == 200) {
        this.categoriesre = categoriesr.data;
        this.article = articleres.data
        var articleData = articleres.data,
            articleDate = [],
            dateList = [];
        console.log(articleData);
        for (let i = 0; i < articleData.length; i++){
            let Arr = articleres.data[i].date;
            articleDate.push(Arr);
        }
        for(let i=0; i<articleDate.length; i++){
          let arrlist = articleDate[i]
          let arrStred = arrlist.substring(0,10)
          dateList.push(arrStred)
        }
        console.log(dateList);
        this.AllDateList = dateList;
      };
   }))
   .catch((error)=>{})
 }

}
</script>
