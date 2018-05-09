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
        cate:[]
      }
    },
    created(){
      axios.all([
        axios.get('http://www.likecn.cn/wp-json/wp/v2/categories')
      ])
        .then(axios.spread((categoriesr)=>{
          // console.log(articleres.data)
          console.log(categoriesr.data[0].name)
          if (categoriesr.status == 200) {
            this.cate = categoriesr.data;
          };
        }))
        .catch((error)=>{})
    }

  }
</script>
