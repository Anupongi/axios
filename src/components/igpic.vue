<template>
    <div id="igpic">
        <form @submit="onSubmit">
        <input type="text" v-model="keyword" id="search"> 
        <button type="submit"  class="button"><i class="fas fa-search"></i> ค้นหา</button>
        </form>
        <div v-for="p in profile" :key="p.id">
            <img :src="p.profile_pic_url" style="border-radius: 50%;">
        </div>
        <h3 v-for="h in hashtag" :key="h.id">{{'# '+ h.name}}</h3>
        <h4 v-if="allPost">{{allpost +  " &nbsp; โพสต์"}} </h4> 
            <div class="container"  v-for="c in ig" :key="c.id">
                <img :src="c.node.display_url" class="image">
                <div class="overlay">
                    <div class="text"  >
                            <div>{{like}}</div> &nbsp; <div><i class="fas fa-comment-alt"></i></div>
                    </div>
                </div>
            </div>
    </div>
</template>

<script>
import axios from 'axios';
export default {
    name: 'igpic',
    data(){
      return{
          ig: [],
          hashtag: []  ,
          like: [],
          keyword:"",
          allpost:[],
          allPost:false,
          profile:[]
      }  
    },
    mounted() {
        this.load();
    },
    methods:{
        load() {
            axios.get('https://www.instagram.com/explore/tags/' + this.keyword + '/?__a=1',null)
            .then(result =>{
                this.ig = result.data.graphql.hashtag.edge_hashtag_to_media.edges;
                this.hashtag = result.data.graphql;
                this.allpost = result.data.graphql.hashtag.edge_hashtag_to_media.count;
                this.allPost = true;
                // this.like = result.data.graphql.hashtag.edge_hashtag_to_media.edges.edge_liked_by.count;
                this.profile =result.data.graphql;
            })

            .catch(error => {
                console.log(error);
            });
        },
        onSubmit(ev) {
            ev.preventDefault();
            this.load()
        }   
    }
}
</script>

<style lang="scss" scoped>
#igpic {
    width:100%;
    
    input[type=text], select {
        width: 30%;
        padding: 8px;
        margin: 8px 0;
        border: 1px solid #ccc;
        border-radius: 4px;
        box-sizing: border-box;
        font-family: 'Kanit', sans-serif;
        font-size: 20px;
    }
    .button {
            font-family: 'Kanit', sans-serif;
            background-color: #4CAF50;
            border: none;
            color: white;
            padding: 15px 32px;
            text-align: center;
            text-decoration: none;
            display: inline-block;
            font-size: 16px;
            margin: 4px 10px;
            cursor: pointer;
            border-radius: 4px;
    }
    h3{
        font-size: 30px;
    }
    
        .container {
            margin: 1.5%;
            padding: 10;
            float: left;
            position: relative;
            width: 30%;
            
            .image {
                display: block;
                width: 100%;
                height: 250px;
            }
            .overlay {
                transition: .5s ease;
                opacity: 0;
                position: absolute;
                top: 0;
                bottom: 0;
                left: 0;
                right: 0;
                background-color: rgb(245, 18, 86);
                height: 100%;
  width: 100%;
            
            }
            .overlay:hover {
                opacity: 1;
            }
            .text {
                color: black;
                font-size: 20px;
                position: absolute;
                top: 50%;
                left: 50%;
                -webkit-transform: translate(-50%, -50%);
                -ms-transform: translate(-50%, -50%);
                transform: translate(-50%, -50%);
                text-align: center;
            } 
    }
}
</style>
