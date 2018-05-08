<template>
  <div>
    <h2>categories 组件</h2>
    <ul>
      <li v-for="(item,i) in cate" :key="i">{{cate[i].name}}</li>
    </ul>
  </div>
</template>


<script>
  import axios from 'axios'
  export default {
    data(){
      return {
        // article:[],
        cate:[]
        // articleTime:[],
        // AllDateList:[]
      }
    },
    created(){
      axios.all([
        // axios.get('http://www.likecn.cn/wp-json/wp/v2/posts'),
        axios.get('http://www.likecn.cn/wp-json/wp/v2/categories')
        // axios.get('http://www.likecn.cn/wp-json/wp/v2/comments')
      ])
        .then(axios.spread((categoriesr)=>{
          // console.log(articleres.data)
          console.log(categoriesr.data[0].name)
          if (articleres.status == 200) {
            this.cate = categoriesr.data;
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
