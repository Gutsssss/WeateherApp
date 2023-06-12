<template>
    <div class="backgorund-search">
    <select class="select" :value="value" @input="updateValue">
    <option class="select-option" v-for="item of cities" :key="item.value">{{ item.name }}</option>
    {{ selected }}
    </select>
<button class="button" @click="getWeather">Получить данные</button>
</div>
</template>

<script setup>
import { defineProps,defineEmits } from 'vue';
const props = defineProps({
    cities: Array,
    value: String
})
const emit = defineEmits(['update:value','getWeather'])
const getWeather = () => {
        emit('getWeather',props.cities)
    }
const updateValue = (event) => {
  emit('update:value',event.target.value)
}
</script>

<style scoped>
.background {
  width: 100%;
  height: 500px;
  margin: auto;
  text-align: center;
}
.backgorund-search {
  display: flex;
  justify-content: center;
  align-items: flex-end;
  gap: 20px;
}
* {
  color: rgb(255, 255, 255);
}
.select {
  width: 300px;
  margin-top: 10px;
  color: rgb(255, 255, 255);
  font-size: 24px;
  background: rgb(104, 89, 241);
  border-radius: 15px;
  text-align: center;
  height: 40px;
}
.select-option {
  background-color: rgb(104, 89, 241);
  border-radius: 10px;
}
.button {
  width: 150px;
  height: 40px;
  border-radius: 15px;
  background: rgb(104, 89, 241);
}
.v-card {
  background-color: rgb(104, 89, 241);
  margin-top: 20px;
  border-radius: 15px;
}
.iconImg {
  widows: 100px;
  height: 100px;
  padding-left: 50px;
}
</style>