<script>
function random_bin () {
  return Math.ceil(Math.random()*500).toString(2);
}
export default {
  data() {
    return {
      opd1: '',
      opd2: '',
      opr: '',
      result: "",
      disabled: false,
      correct: undefined
    };
  },
  created() { this.reset(); },
  methods: {
    eval_answer () {
      let input = this.result.trim();
      if (input == '') return;
      let op1 = parseInt(this.opd1,2), op2 = parseInt(this.opd2,2);
      let res = (this.opr == '+') ? op1 + op2 : op1 - op2;
      this.disabled = true;
      this.correct = (res == parseInt(input,2));
			this.$emit('submit', this.correct);
    },
    handle_input () {
      const input = this.$refs.answerInput;
      const pos = input.selectionStart-1;
      if (pos<0) pos = 0;
      input.setSelectionRange(pos, pos);
    },
    on_focus () {
      this.$refs.answerInput.focus();
    },
    reset () {
      this.opd1 = random_bin();
      this.opd2 = random_bin();
      this.opr = (Math.random()<0.5)?"+":"-";
      this.result = "";
      this.disabled = false;
      this.correct = undefined;
      if (this.opr == '-' && parseInt(this.opd1) < parseInt(this.opd2)) {
        let tmp = this.opd2;
        this.opd2 = this.opd1;
        this.opd1 = tmp;
      }
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
          @input="handle_input"
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