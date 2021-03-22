<template>
  <div id="app">
		<div style="width: 100%;height: 100%;background: pink;">
			<button @click="popup()" style="margin-top: 500px;">点击我弹出判断窗口</button>
		</div>
		
		<Stripe v-if='show' @dialogVisibleEvent="popup"/>
  </div>
</template>

<script>
import Stripe from './common/Stripe/Srtipe.vue'
import PaySuccess from './view/pay/PaySuccess.vue'
import PayCancel from './view/pay/PayCancel.vue'

export default {
  name: 'app',
	data(){
		return {
			show:false
		}	
	},
  components: {
    Stripe,
		PaySuccess,
		PayCancel
  },
	methods:{
		popup(){
			this.show = !this.show
		},
		cancel(){
			alert(1)
		}
	}
}
</script>

<style>
	* {
		margin: 0;
		padding: 0;
	}
	html {
		width: 100%;
		height: 100%;
	}
	body {
		width: 100%;
		height: 100vh;
	}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
 
	height: 100%;
}
</style>
