<template>
  <div class="col-xs-6 text-center">
  	<button class="btn btn-primary margin" @click="isRight()">
  		<slot></slot>
  	</button>
  </div>
</template>

<script>
import { eventBus } from '../main';

export default {
	props: ['rightAns', 'ans'],
	methods: {
		isRight(){
			if (this.rightAns === this.ans) {
				eventBus.$emit('switchRight')
			} else {
				eventBus.$emit('switchError')
			}
		}
	}
}
</script>

<style lang="scss">
	.margin{
		margin: 10px 0;
	}
</style>
