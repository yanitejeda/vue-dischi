<template>
    <div>
        <div class="topBg py-2"> <img class="mw3" :src="require('@/assets/spotify-log.png')" alt=""></div>
        <div class="mainbg py-2" > 

                <div class="py-5">
                    <select class="form-select with20 mx-auto" aria-label="Default select example ">
                        <option selected>scegli genere musicale</option>
                        <option v-for="(value, key) in getGenreList " :key="key">{{key}} n. {{value}}</option>
                    </select>
                </div>
           
            
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
    computed:{
         getGenreList (){

            const genreList = {};


            this.listalbum.forEach((disco)=>{
                const {genre} = disco;

                if(!genreList[genre]) {

                    genreList[genre] = 0;
                }
                    genreList[genre]++;
            });

        console.log( genreList);
        return genreList

        },

    },

    methods:{

       /*  getGenreList (){

            const genreList = {};


            this.listalbum.forEach((disco)=>{
                const {genre} = disco;

                if(!genreList[genre]) {

                    genreList[genre] = 0;
                }
                    genreList[genre]++;
            });

        console.log( genreList);
        return genreList

        }, */
        
    }, 
    
   

   mounted(){

   axios.get("https://flynn.boolean.careers/exercises/api/array/music")
   .then((resp) =>{
       this.listalbum = resp.data.response ;
   })
   },

};
</script>