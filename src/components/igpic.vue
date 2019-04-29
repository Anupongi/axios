<template>
    <div id="igpic">
        <input type="text">
        <ul> 
            <li v-for="c in ig" :key="c.id">
                <div > {{c.node.display_url }}</div>
                <img src="'+  .node.thumbnail_resources.src +'">
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
          ig: []
      }  
    },
    mounted() {
        this.load();
    },
    methods:{
        load() {
            axios.get('https://www.instagram.com/explore/tags/cat/?__a=1',null
            )
            .then(result =>{
                this.ig = result.data.graphql.hashtag.edge_hashtag_to_media.edges;
            })
            .catch(error => {
                console.log(error);
            });
        }
    }
    
}
</script>

<style lang="scss" scoped>

</style>
