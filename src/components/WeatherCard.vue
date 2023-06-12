<template>
    <v-card
    class="mx-auto"
    max-width="300"
  >
  <v-card-title>Weather in {{ city }}</v-card-title>
  
    <v-card-item>
      <template v-slot:subtitle>
       {{ weather }}
       <div id="icon" src='{{img}}'></div>
      </template>
      
    </v-card-item>

    <v-card-text class="py-0">
      <v-row align="center" no-gutters>
        <v-col
          class="text-h2"
          cols="6"
        >
          {{temp}}°
        </v-col>
        <v-col
        class="text-h4"
        >
          {{time}}
        </v-col>
      </v-row>
    </v-card-text>

    <div class="d-flex py-3 justify-space-between">
      <v-list-item
        density="compact"
      >
        <v-list-item-subtitle>Wind {{wind }} m/s</v-list-item-subtitle>
      </v-list-item>

      <v-list-item
        density="compact"
        prepend-icon="mdi-weather-pouring"
      >
        <v-list-item-subtitle>Humidity {{humidity}}</v-list-item-subtitle>
      </v-list-item>
    </div>
  </v-card>
</template>

<script setup>
import { defineProps } from 'vue';
const props = defineProps({
    city:String,
    weather:String,
    temp:Number,
    time:Number,
    wind:Number,
    humidity:String,
    img:String
})
console.log(props)
</script>

<style scoped>
* {
  color: rgb(255, 255, 255);
}

</style>