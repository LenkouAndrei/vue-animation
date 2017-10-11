<template>
	<div class="row margin-top">
	  <div class="wrong-content text-center">
		<h2 class="wrong-content__headline">That's wrong!</h2>
		<hr>
		<button class="btn btn-danger" @click="again()">Try again</button>
	  </div>
	</div>
</template>

<script>
import { eventBus } from '../main';

export default {
	methods: {
		again() {
			eventBus.$emit('stay')
		}
	}
}
</script>

<style lang="scss" scoped>
.wrong-content{
	background: #dca2a1;
	padding: 20px 0;
	border-radius: 10px;

	&__headline{
		color: darken(#dca2a1, 30);
	}
}
.margin-top{
	margin-top: 10px;
}
</style>
