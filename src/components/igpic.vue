<template>
    <div id="igpic">
        <input type="text" v-model="keyword"> <button type="submit" class="button"><i class="fas fa-search"></i> ค้นหา</button>
        <h3 v-for="h in hashtag" :key="h.id">{{'#'+ h.name}}</h3>
        <ul class="pic_all"> 
            <li v-for="c in ig" :key="c.id" style="list-style-type: none;  ">
                <img class="pic" :src="c.node.display_url">
            </li>
        </ul>
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
          keyword:""
      }  
    },
    mounted() {
        this.load();
    },
    methods:{
        load() {
            axios.get('https://www.instagram.com/explore/tags/cats/?__a=1',null
            )
            .then(result =>{
                this.ig = result.data.graphql.hashtag.edge_hashtag_to_media.edges;
                this.hashtag = result.data.graphql;    
            })
            .catch(error => {
                console.log(error);
            });
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
    .pic_all {
        margin: 0; 
        padding: 0;
        .pic{
            width: 200px;
            height: 250px;
            width: 25%;
            margin: 1.5%;
            padding-left:  50px;
            float: left;
            position: relative;
        }   
    }
}
</style>
