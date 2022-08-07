<script lang="ts">
export default {
	data () {
		return {
			base1: 0,
			base2: 0,
			number: '',
			correct: 2,
			disabled: false,
			result: ""
		};
	},
	created() { this.reset(); },
	methods: {
		eval_answer () {
			let input = this.result.trim();
			if (input == '') return;
			this.disabled = true;
			this.correct = (parseInt(this.number,this.base1) == parseInt(input,this.base2))?1:0;
			this.$emit('submit', this.correct);
		},
		on_focus () {
			this.$refs.answerInput.focus();
		},
		reset () {
			this.base1 = (Math.random()<0.5)?8:16;
			this.base2 = (this.base1==8)?16:8;
			this.number = Math.ceil(Math.random()*5000).toString(this.base1);
			this.correct = 2;
			this.disabled = false;
			this.result = "";
		}
	}
}
</script>
<template>
	<p class="item">
		{{number}}<sub>{{base1}}</sub> =
		<input v-model="result" placeholder="Answer" class="item" ref="answerInput"
			v-on:keyup.enter="eval_answer"
			:disabled="disabled"
			style="width:16rem;" /><sub>{{base2}}</sub>
		<span style="color:green" v-if="correct==1">✔</span>
		<span style="color:red" v-else-if="correct==0">✘</span>
		<span style="color:rgba(0,0,0,0)" v-else>✔</span>
	</p>
</template>

<style scoped>
.item {
	font-size: 2rem ;
	font-family: consolas;
}
p.item {
	margin-left: 2rem;
}
input.item {
	text-align: right;
}
.item > sub {
	color: gray;
	font-size: 1rem;
}
</style>