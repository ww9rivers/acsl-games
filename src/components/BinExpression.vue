<script>
function random_bin () {
  return Math.ceil(Math.random()*500).toString(2);
}
export default {
  data() {
    const x = {
      opd1: random_bin(),
      opd2: random_bin(),
      opr: (Math.random()<0.5)?"+":"-",
      result: "",
      disabled: false,
      correct: undefined
    };
    if (x.opr == '-' && parseInt(x.opd1) < parseInt(x.opd2)) {
      let tmp = x.opd2;
      x.opd2 = x.opd1;
      x.opd1 = tmp;
    }
    return x;
  },
  methods: {
    eval_answer () {
      let input = this.result.trim();
      if (input == '') return;
      let op1 = parseInt(this.opd1,2), op2 = parseInt(this.opd2,2);
      let res = (this.opr == '+') ? op1 + op2 : op1 - op2;
      this.correct = (res == parseInt(input,2));
      this.disabled = true;
    },
    on_focus () {
      this.$refs.answerInput.focus();
    }
  }
}
</script>

<template>
  <table class="item" @click="on_focus">
    <tr><td></td><td><span class="operand">{{ opd1 }}</span></td></tr>
    <tr><td>{{ opr }}</td><td><span class="operand">{{ opd2 }}</span></td></tr>
    <tr>
      <td>
        <button style="font-size:1.5rem;" data-title="Click to submit answer"
          :disabled="disabled"
          @focus="on_focus"
          @click="eval_answer">=</button>
      </td>
      <td style="border-top: 2px solid black">
        <input v-model="result" placeholder="Answer" class="item" ref="answerInput"
          v-on:keyup.enter="eval_answer"
          :disabled="disabled"
          :style="{ 'width': (Math.max(opd1.length, opd2.length)+3) + 'rem' }" />
      </td>
      <td>
        <span style="color:green" v-if="correct">✔</span>
        <span style="color:red" v-else-if="correct===false">✘</span>
        <span style="color:rgba(0,0,0,0)" v-else>✔</span>
      </td>
    </tr>
  </table>
</template>

<style scoped>
.item {
  text-align: right;
  font-size: 2rem ;
  font-family: consolas;
}
table.item {
  border: 0;
  display: inline-table;
  margin-left: 2rem;
  margin-bottom: 12pt;
}
table.item > tr {
  line-height: 1;
}
.operand {
  margin-right: 5px;
}
</style>