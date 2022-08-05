<script setup lang="ts">
import BinExpression from '@/components/BinExpression.vue';
import HexAndOctal from '@/components/HexAndOctal.vue';
import { def } from '@vue/shared';
</script>

<script lang="ts">
export default {
  methods: {
    reset_game () {
      window.alert("To restart the game.");
    }
  }
}
</script>

<template>
  <div class="games">
    <h1>ACSL Games</h1>
    <p>
      ACSL curriculum relevant games.
    </p>
    <h2>Number System</h2>
    <h3>Binary</h3>
    <button style="font-size:1.5rem;" @click="reset_game" data-title="Click to restart">🔄</button>
    <div id="bin">
      <BinExpression v-for="ix in 6" :key="ix" :id="'bin_'+ix" />
    </div>
    <h3>Hexadecimal and Octal</h3>
    <div id="octal">
      <HexAndOctal v-for="ix in 6" :key="ix" :id="'oct_'+ix" />
    </div>
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
