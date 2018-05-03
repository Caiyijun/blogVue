<template>
<div class="layout">
  <Layout>
      <Header :style="{position: 'fixed', width: '100%'}">
          <Menu mode="horizontal" theme="dark" active-name="1">
              <div class="layout-logo"></div>
              <div class="layout-nav">
                  <MenuItem name="1">
                      <Icon type="ios-navigate"></Icon>
                      Item 1
                  </MenuItem>
              </div>
          </Menu>
      </Header>
      <Content :style="{margin: '88px 20px 0', background: '#fff', minHeight: '500px'}">
          </nuxt>
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
     axios.get('http://www.likecn.cn/wp-json/wp/v2/comments')
   ])
   .then(axios.spread((articleres,categoriesres,commentsres)=>{
    //  console.log(articleres.data);
     console.log(commentsres)
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
html {
  font-family: "Source Sans Pro", -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
  font-size: 16px;
  word-spacing: 1px;
  -ms-text-size-adjust: 100%;
  -webkit-text-size-adjust: 100%;
  -moz-osx-font-smoothing: grayscale;
  -webkit-font-smoothing: antialiased;
  box-sizing: border-box;
}

*, *:before, *:after {
  box-sizing: border-box;
  margin: 0;
}

.button--green {
  display: inline-block;
  border-radius: 4px;
  border: 1px solid #3b8070;
  color: #3b8070;
  text-decoration: none;
  padding: 10px 30px;
}

.button--green:hover {
  color: #fff;
  background-color: #3b8070;
}

.button--grey {
  display: inline-block;
  border-radius: 4px;
  border: 1px solid #35495e;
  color: #35495e;
  text-decoration: none;
  padding: 10px 30px;
  margin-left: 15px;
}

.button--grey:hover {
  color: #fff;
  background-color: #35495e;
}


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
        width: 420px;
        margin: 0 auto;
        margin-right: 20px;
    }
    .layout-footer-center{
        text-align: center;
    }
</style>
