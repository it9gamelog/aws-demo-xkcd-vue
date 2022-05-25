<script setup>
import { ref } from 'vue';
const api = import.meta.env.VITE_API;
const output = ref("");

async function rollDice() {
  output.value = "Rolling...";
  const resp = await fetch(`${api}/dice`);
  output.value = await resp.text();
}

async function geohash() {
  output.value = "Loading...";
  const dateval = document.querySelector('#geodate').value;
  const resp = await fetch(`${api}/geohash/${dateval}`);
  const val = await resp.json();
  output.value = JSON.stringify(val, null, 2);
}
</script>

<template>
  <h2>Roll</h2>
  <button @click="rollDice()">Roll Dice!</button>

  <h2>Geohashing</h2>
  <input type="date" id="geodate" @change="geohash()">

  <h2>Output</h2>
  <pre>{{ output }}</pre>
</template>

