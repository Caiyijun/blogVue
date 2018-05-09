<template>
    <div>
        <div class="article-body">
            <h2>文章</h2>
            <!-- <p>id:{{ $route.params.id }}</p> -->
            <!-- <p>{{id}}</p> -->
            <span class="time-tip">{{articleData}}</span>
            <div class="article-pere">
                <p v-html=" (content)"></p>
            </div>
        </div>
    </div>
</template>

<script>
    import axios from 'axios'
    export default {
        head(){
            return {
                title:'文章'
            }
        },
        data(){
            return {
                id: this.$route.params.id,
                articleData:'',
                content:'',
                title:''
            }
        },
        created(){
            this.getarticle()
        },
        methods:{
            getarticle(){
                axios.get('http://www.likecn.cn/wp-json/wp/v2/posts/' + this.id)
                    .then(res=>{
                        console.log(res.data);
                       this.date =  res.data.date,
                       this.content = res.data.content.rendered,
                       this.title = res.data.title.rendered
                       var articleDate = res.data.date,
                            sDate = articleDate.substring(0,10);
                        console.log(sDate);
                        this.articleData = sDate
                    })
                }
            }
        }
</script>

<style scoped>

</style>