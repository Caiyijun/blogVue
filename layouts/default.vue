<template>
<div class="layout">
  <Layout>
      <Header :style="{position: 'fixed', width: '100%'}">
          <Menu mode="horizontal" theme="dark" active-name="1">
              <div class="layout-logo"></div>
              <div class="layout-nav">
                  <MenuItem name="1">
                      <Icon type="ios-navigate"></Icon>
                      <nuxt-link :to="{name:'index'}">首页</nuxt-link>
                  </MenuItem>
                  <MenuItem name="1" v-for="(item,i) in categories" :key="i">
                      <Icon type="ios-navigate"></Icon>
                      <nuxt-link :to="{name:'categorie-id',params:{id:categories[i].id}}">{{ categories[i].name }}</nuxt-link>
                  </MenuItem>
              </div>
          </Menu>
      </Header>
      <Content :style="{margin: '88px 20px 0', background: '#fff', minHeight: '500px'}">
          <nuxt/>
      </Content>
      <Footer class="layout-footer-center">2011-2016 &copy; TalkingData</Footer>
  </Layout>
</div>
</template>

<script>
import axios from 'axios'

export default {
  data(){
    return {
      isCollapsed: false,
      article:[],
      categories:[]
    }
  },
 created(){
   axios.all([
     axios.get('http://www.likecn.cn/wp-json/wp/v2/posts'),
     axios.get('http://www.likecn.cn/wp-json/wp/v2/categories'),
   ])
   .then(axios.spread((articleres,categoriesres,commentsres)=>{
    //  console.log(articleres.data);
    //  console.log(commentsres)
     if (articleres.status == 200) {
       this.article = articleres.data,
       this.categories = categoriesres.data
     }
   }))
   .catch((error)=>{})
 },
 computed: {
    menuitemClasses: function () {
      return [
          'menu-item',
          this.isCollapsed ? 'collapsed-menu' : ''
      ]
    }
  }
  
}
</script>


<style>
.layout{
        border: 1px solid #d7dde4;
        background: #f5f7f9;
        position: relative;
        border-radius: 4px;
        overflow: hidden;
    }
.layout-logo{
    width: 100px;
    height: 30px;
    background: #5b6270;
    border-radius: 3px;
    float: left;
    position: relative;
    top: 15px;
    left: 20px;
}
.layout-nav{
    margin: 0 auto;
    margin-right: 20px;
    float: right;
}
.layout-footer-center{
    text-align: center;
}
</style>
