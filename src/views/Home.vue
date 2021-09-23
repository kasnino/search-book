<template>
  <div>
    <v-row class="mt-8 justify-center pa-0 ma-0 " style="width:100%; ">
      <v-col cols="12" md="8" lg="8" class=" text-center ">
        <span class="titulo">Search-Book</span>
      </v-col>
      <v-col
        cols="12"
        md="9"
        lg="9"
        class=""
        :class="{
          'justify-center': $vuetify.breakpoint.xsOnly,
        }"
      >
        <search-bar v-on:tengo_resultados="onResultados"></search-bar>
      </v-col>
    </v-row>
    <v-row class=" justify-center pa-0 ma-0 " style="width:100%; ">
      <v-col cols="12" md="8" lg="8" class=" text-left ">
        <v-row class=" justify-center pa-0 ma-0  " style="width:100%; ">
          <v-col cols="12" md="11" lg="11" class=" text-left pa-0  ">
            <span class="grey--text">Resultados</span>
            <v-divider class="mt-2" color="#eaeaea"></v-divider>
          </v-col>
              <v-col
            cols="12"
            xs="12"
            sm="10"
            md="10"
            lg="10"
            v-if="!loading"
            class="pa-0 ma-0  mt-5 align-center d-flex justify-center"
          >
            Cargando data...
          </v-col>
            <v-col
            cols="12"
            sm="11"
            md="11"
            lg="11"
            class=" ma-0  align-center d-flex justify-center"
          >
          <card-book :book="listBooks.docs"></card-book>
            </v-col>
        </v-row>
      </v-col>
    </v-row>
  </div>
</template>

<script>
import cardBook from "../components/cardBook"
import axios from "axios";
export default {
  name: "Home",

  components: {cardBook},
  data() {
    return {
      listBooks: [],
      palabra:'',
      pagination: {
        pages: 1,
        total: 0,
      },
      RespaldoAllData: [],
      uploadPercentage: 0,
      loading: true,
    };
  },

  methods: {
    onResultados(data){
      this.palabra = data
      this.TodosDatos();
    },
    TodosDatos() {
      console.log("peticion a la api http://openlibrary.org/search.json?author="+this.palabra+"&page=2")
      axios
        .get("http://openlibrary.org/search.json?author="+this.palabra, {
          onDownloadProgress: (progressEvent) => {
            let percentCompleted = Math.round(
              (progressEvent.loaded * 100) / progressEvent.total
            );
          },
        })
        .then((result) => {
          console.log(result.data);
          this.listBooks = result.data;
          console.log(this.listBooks.docs[0]);
          this.loading = false;
          console.log("entro"+this.palabra)
        });

    },
  },
};
</script>
<style lang="scss" scoped>
.card__show--caricatura {
  border-radius: 10px !important;
  border: 1px solid #e0e0e0;
  cursor: pointer;
}

.titulo{
   font-family: muli;
   font-size: 40px;
   color:#666666;
}
</style>
