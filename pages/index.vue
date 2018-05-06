<template>
  <div>

    <ul class="article-list">
      <li v-for="(item,i) in article" :key="i">
        <!-- <nuxt-link :to="{name:'article-id',params:{id:article[i].id}}" > -->
          <h2>{{ article[i].title.rendered }}</h2>
          <p v-html="( article[i].excerpt.rendered )"></p>
          <span>时间：{{ AllDateList[i] }}</span>
          <span>www---{{article[i].categories[0]}}</span>
          <span v-for="(items,index) in categoriesre" :key="index">
            <!-- {{ categoriesre[article[i].categories[0]].name }} -->
            <!-- {{ categoriesre[index].name }}1212 -->
          </span>
        <!-- </nuxt-link> -->
      </li>
    </ul>
    <!-- <ul class="article-list">
      <li v-for="(item,i) in categoriesre" :key="i">
        <span>{{ categoriesre[i].id }}---{{ categoriesre[i].name }}</span>
        <ul>
          <li v-for="(items,index) in article" :key="index">
              <h2>{{ article[categoriesre[i].id].title.rendered }}</h2>
          </li>
        </ul> -->
        <!-- <nuxt-link :to="{name:'article-id',params:{id:article[i].id}}" > -->
          <!-- <h2>{{ article[i].title.rendered }}</h2>
          <p v-html="( article[i].excerpt.rendered )"></p>
          <span>时间：{{ article[i].modified }}</span>
          <span>时间：{{ article[i].modified }}</span>
          <span>www---{{article[i].categories[0]}}</span>
          <span v-for="(items,index) in categoriesre" :key="index"> -->
            <!-- {{ categoriesre[article[i].categories[0]].name }} -->
            <!-- {{ categoriesre[index].name }}1212 -->
          <!-- </span> -->
        <!-- </nuxt-link> -->
      <!-- </li>
    </ul> -->
    <!-- <h2>分类列表</h2>
    <ul>
      <li v-for="(item,i) in categories" :key="i">
        <nuxt-link :to="{name:'categorie-id',params:{id:categories[i].id}}">{{ categories[i].name }}</nuxt-link>
      </li>
    </ul> -->
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
    // console.log(categoriesr.data)
     if (articleres.status == 200) {
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
