<template>
  <v-app dark>
    <v-app-bar
      app
      color="primary"
      dark
    >
      <div class="d-flex align-center">
        <v-img
          alt="Vuetify Logo"
          class="shrink mr-2"
          contain
          src="@/assets/open-book-svgrepo-com.svg"
          transition="scale-transition"
          width="40"
        />

       
      </div>

      <v-spacer></v-spacer>

    
    </v-app-bar>

    <v-main>
      <router-view/>
    </v-main>
  </v-app>
</template>

<script>

export default {
  name: 'App',

  data: () => ({
    //
  }),
};
</script>

<style lang="scss" >
@import "./sass/variables";
input{ 
margin-left: 10px !important;
}

@font-face {
  font-family: muli;
  src: url("./assets/Muli.ttf");
}

</style>
