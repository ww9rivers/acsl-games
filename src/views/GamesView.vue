<script setup lang="ts">
import BinExpression from '@/components/BinExpression.vue';
</script>
<script lang="ts">
export default {
  methods: {
    add_game () {
      window.alert("To add an item");
    }
  }
}
</script>

<template>
  <div class="games">
    <h1>ACSL Games</h1>
    <p>
      ACSL curriculum relavent games.
    </p>
    <h2>Number System</h2>
    <h3>Binary</h3>
    <div id="bin">
      <BinExpression />
      <button style="font-size:1.5rem;" @click="add_game" data-title="Click to add new item">»</button>
    </div>
    <h3>Octal</h3>
    <h3>Hexadecimal</h3>
  </div>
</template>

<style>
@media (min-width: 1024px) {
  .games {
    min-height: 100vh;
    display: flex;
    align-items: center;
  }
}
</style>
