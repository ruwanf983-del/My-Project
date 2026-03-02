<script setup lang="ts">
import Countbutton from "./components/Countbutton.vue"

var message = ref("Good Morning");
var count = ref(0);

function incrementCount() {
  count.value++;
}
</script>

<template>
    <h1>{{ message }}</h1>
    <button class = "vue-button" @click="incrementCount()">Click Me : {{count}}</button>
    <Countbutton />
</template>

<style scoped>
h1{
  color: rebeccapurple;
}
</style>