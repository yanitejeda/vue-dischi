<template>
    <div>
        <div class="topBg py-2"> <img class="mw3" :src="require('@/assets/spotify-log.png')" alt=""></div>
        <div class="mainbg py-2" > 
            <SelecGenre>
                
            </SelecGenre>
            <div class="row row-cols-1 row-cols-md-5 g-4 container mx-auto ">
                    <div class="col d-flex text-center" v-for="(disco, i) in listalbum" :key="i">
                        <DiscoCard 
                        :author="disco.author"
                        :genre="disco.genre"
                        :poster="disco.poster"
                        :title="disco.title"
                        :year="disco.year"
                        >

                        </DiscoCard>
                   
                </div>
            </div>

        </div>
    </div>
</template>
<script>
import axios from "axios";
import DiscoCard from "./DiscoCard.vue";
import SelecGenre from "./SelecGenre.vue"

export default {
   name:"DiscContainer",
   components:{DiscoCard,SelecGenre },

   data(){
       return{
           listalbum:[]
       }

   },

   mounted(){
   axios.get("https://flynn.boolean.careers/exercises/api/array/music")
   .then((resp) =>{
       this.listalbum = resp.data.response ;
   })
   },

};
</script>