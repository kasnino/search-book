<template>
  <div>
    <v-row class="mt-8 justify-center pa-0 ma-0 " style="width:100%; ">
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
          <v-col cols="12" md="10" lg="10" class=" text-left pa-0  ">
            <span class="grey--text">Resultados</span>
            <v-divider class="mt-2" color="#eaeaea"></v-divider>
          </v-col>

          <v-col
            cols="12"
            xs="12"
            sm="10"
            md="10"
            lg="10"
            v-if="loading"
            class="pa-0 ma-0  mt-5 align-center d-flex justify-center"
          >
            Cargando data...
          </v-col>
          <v-col
            cols="10"
           xs="6"
            sm="6"
            md="6"
            lg="6"
            v-else
               v-for="(item, index) in listBooks.docs"
            :key="index"
            class=" ma-0  align-center d-flex justify-center"
          >
              <template>
              <v-card
                class="mx-auto card__show--caricatura elevation-4"
                style="border-radius:16px;background:var(--card__fondo);"
            
                outlined
                :class="`animated fadeIn dura-${index}`"
                @click="ShowModal(), personajeModal(item)"
              >
                <v-row class=" pa-0 ma-0">
                  <v-col cols="4" md="4" style="background:#eaeaea;" class="  justify-center align-center ">
                    
                      <div class="Avatar__favorito--btn ">
                        <v-img
                          src="@/assets/open-book-svgrepo-com.svg"
                          width="100px"
                          class="favorite__caricatura ma-0  ml-3"
                          style="border-radius:10px !important;"
                          contain
                        >
                        </v-img>
                      </div>
                  
                  </v-col>

                  <v-col cols="8" md="8" class="  pa-1 ma-0">
                    <v-list-item three-line class="pa-0 ma-0 ml-2">
                      <v-list-item-content class="pa-0 ma-0 mt-3">
                        <div style="line-height:17px; " class="ma-1">
                        
                            <v-badge
                              bordered
                              color="success"
                              dot
                              left
                            inline
                            >
                                <v-list-item-title
                            class="texto__card--name pa-0 ma-0  black--text"
                          >
                          {{item.title}}
                          </v-list-item-title>
                            </v-badge>
                         
                        
                        </div>

                        <div style="line-height:12px; " class="ma-1">
                          <v-list-item-subtitle
                            class="texto__card--subdescription" style="color:var(--texto--titulo-topcard);"
                            >Last known location:
                          </v-list-item-subtitle>
                          <v-list-item-title
                            class="texto__card--sublocation pa-0 ma-0 "
                          >
                           sgdfgd
                          </v-list-item-title>
                        </div>

                        <div style="line-height:12px; " class="ma-1">
                          <v-list-item-subtitle
                            class="texto__card--subdescription" style="color:var(--texto--titulo-topcard);"
                            >First seen in:
                          </v-list-item-subtitle>
                          <v-list-item-title
                            class="texto__card--sublocation pa-0 ma-0 "
                          >
                            Never Ricking Morty
                          </v-list-item-title>
                        </div>
                      </v-list-item-content>
                    </v-list-item>
                  </v-col>
                </v-row>
              </v-card>
            </template>
          </v-col>
        </v-row>
      </v-col>
    </v-row>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "Home",

  components: {},
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
      console.log("peticion a la api http://openlibrary.org/search.json?author="+this.palabra)
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
</style>
