<template>
    <div>
        <h2>文章</h2>
        <p>id:{{ $route.params.id }}</p>
        <p>{{id}}</p>
        <p>{{date}}</p>
        <p v-html=" (content)"></p>
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
                date:'11',
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
                        console.log(res.data.title.rendered);
                       this.date =  res.data.date,
                       this.content = res.data.content.rendered,
                       this.title = res.data.title.rendered
                    })
                }
            }
        }
</script>

<style scoped>

</style>