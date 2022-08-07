<script setup lang="ts">
import BinExpression from '@/components/BinExpression.vue';
import HexAndOctal from '@/components/HexAndOctal.vue';
import Timer from '@/components/Timer.vue';
import RefreshIcon from '@/components/icons/IconRefresh.vue';
</script>

<script lang="ts">
export default {
  components: {
    Timer
  },
  data () {
    return {
      total: 6 + 6,
      correct: 0,
      wrong: 0
    }
  },
  methods: {
    on_submit (correct: Boolean) {
      if (correct) { ++this.correct } else { ++this.wrong };
      if (this.correct+this.wrong >= this.total) {
        this.$refs.timer.timer_on = false;
      }
    },
    reset_game () {
      if (this.correct<1 && this.wrong<1 || window.confirm("Reset this game?")) {
        this.correct = this.wrong = 0;
        for (let ref in this.$refs) {
          let xref = this.$refs[ref];
          if (xref instanceof Array) {
            for (let ix of xref) ix.reset();
          } else xref.reset();
        }
      }
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

    <p>
      <RefreshIcon @click="reset_game" data-title="Reset game" /><Timer ref="timer" />
      {{correct}} <span v-if="wrong>0" class="wrong">: {{wrong}}</span>
    </p>

    <h3>Binary</h3>
    <div id="bin">
      <BinExpression @submit="on_submit"
        v-for="ix in 6" :key="ix" ref="bin" />
    </div>
    <h3>Hexadecimal and Octal</h3>
    <div id="octal">
      <HexAndOctal @submit="on_submit"
        v-for="ix in 6" :key="ix" ref="hexoct" />
    </div>
  </div>
</template>

<style scoped>
@media (min-width: 1024px) {
  .games {
    min-height: 100vh;
    display: flex;
    align-items: center;
  }
}
.games > p {
  margin-left: 2rem;
}
.wrong {
  color: red;
}
</style>
