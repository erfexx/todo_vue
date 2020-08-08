<template>
  <v-app>
    <v-app-bar app color="primary" dark>
      <v-toolbar-title>Todo App</v-toolbar-title>
    </v-app-bar>

    <v-content>
      <v-container fluid>
        <!-- jika menggunakan vue-router -->
        <router-view></router-view>
      </v-container>
    </v-content>

    <v-card>
      <v-footer absolute app>
        <v-card-text class="text-center">
          &copy; {{ new Date().getFullYear() }} 
          <strong>Todo-App</strong>
        </v-card-text>
      </v-footer>
    </v-card>
  </v-app>
</template>
<script>
export default {
  name: "App",
};
</script>
