<template>
  <div id = "show-blog">
      <h1 class="blogh1">All Blog Articles</h1>
      <input type="text" v-model="search" placeholder="search blogs">
      <div v-for="blog in filteredBlogs" class="single-blog">
          <router-link v-bind:to="'/blog/'+ blog.id"><h2 v-rainbow>{{blog.title}}</h2></router-link>
          <article>{{blog.content | snippet}}</article>
      </div>
    
    
  </div>
</template>

<script>


export default {
  components:{
    
  },
  
 
  data () {
    return {
      blogs:[],
      search:''
    }
  },
  
  methods:{

  },
  created() {
        this.$http.get('Your firebase realtime database api ==> for example https:/**************.firebaseio.com/posts.json ').then(function(data){
            return data.json();
        }).then(function(data){

            var blogsArray =[];
            for (let key in data){
                data[key].id =key;
                blogsArray.push(data[key]);
            };
            this.blogs = blogsArray;
        })
  },
  computed:{
      filteredBlogs: function(){
          return this.blogs.filter((blog)=>{
              return blog.title.toLowerCase().match(this.search.toLowerCase());
          })
      }
  }
}
</script>

<style>
.blogh1{
    text-align: center;
}
#show-blog{
    max-width: 800px;
    margin: 0px auto;
}
.single-blog{
    padding: 20px;
    margin: 20px 0;
    box-sizing: border-box;
    background: #eee;
}
</style>