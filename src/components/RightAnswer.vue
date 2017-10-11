<template>
	<div class="row">
	  <div class="right-content text-center">
		<h2 class="right-content__headline">That's correct!</h2>
		<hr>
		<button class="btn btn-primary" @click="nextQuestion()">Next Question</button>
	  </div>
	 </div>
</template>

<script>
import { eventBus } from '../main';

export default {
	methods: {
		nextQuestion() {
			eventBus.$emit('next')
		}
	}
}
</script>

<style lang="scss" scoped>
.right-content{
	background: #d6e9c6;
	padding: 20px 0;
	border-radius: 10px;

	&__headline{
		color: darken(#d6e9c6, 60);
	}
}
</style>
