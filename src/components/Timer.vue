<script lang="ts">
export default {
	data () {
		return {
			min: 0,
			sec: 0,
			hilite: true,
			delim_color: '#202020',
			timer_on: true,
			timeoutID: undefined
		}
	},
	methods: {
		high_light () {
			if (!this.timer_on) return;
			if (this.hilite = !this.hilite) {
				this.delim_color = '#00bd7e';
				if (++this.sec > 59) {
					this.sec = 0;
					++this.min;
				}
			} else {
				this.delim_color = '#202020';
			}
			this.timeoutID = setTimeout(this.high_light, 500);
		},
		reset () {
			if (this.timeoutID !== undefined) {
				clearTimeout(this.timeoutID);
			}
			this.min = this.sec = 0; this.timer_on = true;
			this.high_light();
		}
	},
	mounted() {
		setTimeout(this.high_light, 500);
	}
}
</script>

<template>
<div class="timer"><b>{{min}}<span v-bind:style="{ color: delim_color }">:</span><span v-if="sec<=9">0</span>{{sec}}</b></div>
</template>

<style scoped>
div.timer {
	display: inline;
	margin: 0 0 16px 1rem;
	border: solid 1px hsla(160, 100%, 37%, 1);
	border-radius: 5px;
	font-family: Consolas;
	font-size: 2rem;
}
div.timer > b {
	margin: 2px 4px;
}
</style>