<template>
  <div>
    <div class="topBg py-2">
      <img class="mw3" :src="require('@/assets/spotify-log.png')" alt="" />
    </div>
    <div class="mainbg py-2">

      <div class="py-5">
        <select v-model="selectTipe"
          class="form-select with20 mx-auto"
          aria-label="Default select example "
        >
          <option selected>scegli genere musicale</option>
          <option
            v-for="(value, key) in getGenreList"
            :key="key"
            :value="key"
          >
            {{ key }}
          </option>
        </select>
      </div>


      <div class="row row-cols-1 row-cols-md-5 g-4 container mx-auto">
        <template v-for="(disco, i) in listalbum">
            <div
                class="col d-flex text-center"
                :key="i"
                v-if="disco.genre == selectTipe"
            >
            <DiscoCard 
                :author="disco.author"
                :genre="disco.genre"
                :poster="disco.poster"
                :title="disco.title"
                :year="disco.year">
            </DiscoCard>
            </div>
        </template>
      </div>
    </div>
  </div>
</template>
<script>
import axios from "axios";
import DiscoCard from "./DiscoCard.vue";

export default {
  name: "DiscContainer",
  components: { DiscoCard },

  data() {
    return {
      selectTipe: "",
      listalbum: [],
    };
  },
  computed: {
    getGenreList() {
      const genreList = {};

      this.listalbum.forEach((disco) => {
        const { genre } = disco;

        if (!genreList[genre]) {
          genreList[genre] = 0;
        }
        genreList[genre]++;
      });

      console.log(genreList);
      return genreList;
    },
  },

  

  mounted() {
    axios
      .get("https://flynn.boolean.careers/exercises/api/array/music")
      .then((resp) => {
        this.listalbum = resp.data.response;
      });
  },
};
</script>