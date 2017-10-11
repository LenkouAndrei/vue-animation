<template>
	<div>
		<div class="row" v-for="(question, index) in questions" v-if="index === current" :key="index">
		  <div class="panel panel-primary" v-for="(value, key, index) in question" :key="index">
		  	<div class="panel-heading text-center">
		  		<h2 class="panel-title">{{ key }}</h2>
		  	</div>
		  	<div class="panel-body">
			  	<div class="row">
			  		<app-option v-for="(answer, index) in value" :key="index" :rightAns="rightAnswer" :ans="answer">
			  			{{ answer }}
			  		</app-option>
			  	</div>  		
		  	</div>
		  </div>
		</div>
	 </div>
</template>

<script>
  import Option from './Option.vue';
  import { eventBus } from '../main';

  export default {
  	props:['current'],
    components: {
      appOption: Option
    },
    data(){
    	return {
    		questions: [
    		  {'36 + 69' : [105, 200, 211, 816]},
    		  {'20 - 15' : [10, 8, 5, 3]},
    		  {'11 - 20' : [0, -9, 12, 6]},
    		  {'0 + 7' : [11, 70, 6, 7]}
    		]
    	}
    },
    computed: {
    	rightAnswer(){
    		let arr = Object.keys(this.questions[this.current])[0].split(' '),
    			answ;
    		function basicOp(op, v1, v2) {
    		  switch(op){
    		    case '+': return Number(v1) + Number(v2);
    		    case '*': return v1 * v2;
    		    case '-': return v1 - v2;
    		    case '/': return v1 / v2;
    		  }
    		};
    		answ = basicOp(arr[1], arr[0], arr[2]);
    		return answ
    	}
    }
  }
</script>

<style lang="scss" scoped>
</style>