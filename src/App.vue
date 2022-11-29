<template>
  <v-app :theme="theme">
    <v-app-bar color="green">
      <v-app-bar-nav-icon></v-app-bar-nav-icon>
      <v-app-bar-title>Vuetify Demo</v-app-bar-title>
      <v-spacer></v-spacer>
      <v-btn
        :prepend-icon="
          theme === 'light' ? 'mdi-weather-sunny' : 'mdi-weather-night'
        "
        @click="onClick"
        >Toggle Theme</v-btn
      >
    </v-app-bar>
    <v-main>
      <v-container fluid
        ><v-text><h2>Attractions</h2></v-text>
        <v-row>
          <v-col v-for="items in items" cols="12" sm="4">
            <v-card>
              <v-img
                :src="items.coverimage"
                height="200px"
                class="align-end"
                cover
              >
                <v-card-title
                  class="text-white"
                  v-text="items.name"
                ></v-card-title>
              </v-img>
              <v-card-text v-text="items.detail"></v-card-text
              ><v-divider></v-divider>
              <v-card-actions><v-btn>Learn More</v-btn></v-card-actions>
            </v-card>
          </v-col>
        </v-row>
      </v-container>
    </v-main>
  </v-app>
</template>

<script setup>
import { ref } from "vue";

const theme = ref("light");

function onClick() {
  theme.value = theme.value === "light" ? "dark" : "light";
}
const items = ref([]);
fetch("https://www.melivecode.com/api/attractions")
  .then((res) => res.json())
  .then((result) => {
    items.value = result;
    console.log(result);
  });
</script>
