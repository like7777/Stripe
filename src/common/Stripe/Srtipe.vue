<template>
	<div id="mask-layer">
		<div style="width: 200px;
								height: 200px;
								position: absolute;
								background: red;
								left: 50%;
								top: 50%;
								transform: translate(-50%,-90%);">
			<button id="checkout-button" @click="payment()" 
				style="position: absolute;		
				left: 50%;
				top: 50%;
				transform: translate(-50%,-90%);">去付款</button>
				<button @click="cancel()">取消购买</button>
		</div>	
	</div>
</template>

<script>
	const axios = require('axios');
	export default{
		name:'Stripe',	
		props:{
			show : false
		},
		data(){
			return {
				data:{
					  "field": "session_create",
					    "payload": {
					      "cancel_url":"https://example.com/cancel",//请求失败的地址
					      "client_reference_id": "1234",
					      "line_items": [
					        {
					          "amount": 300,
					          "currency": "TOP",
					          "description": "一个月会员",
					          "images": [
					            "https://stripe.com/img1"
					          ],
					          "name": "会员",
					          "quantity": 1
					        }
					      ],
					      "payment_intent_data": {
					        "receipt_email": "1748031151@qq.com.com"
					      },
					      "payment_method_types": [
					        "card"
					      ],
					      "success_url": "https://example.com/success"
					    },
							"demo":{
								"test1":"这是显示套餐",
								"test2":"这是显示信息"
							}
					  },
						response :''
			}
			},
		
		methods:{
			payment(){		 		
				var stripe = Stripe('pk_test_51IVtzyA687uwf9567HM4NnxPdZiTjXpGa1NoEa0cAhAGK7cgpolBiwicW5RseKmZREyvts792GLGx0q6NRWicyGP00kYM7YqAB')
				//console.log(stripe)
				//调用后端的接口
				axios.post('https://jqp8o5g3v3.execute-api.us-west-2.amazonaws.com/dev/epay',this.data
				).then(function (response) {
								console.log(response.data.body)
								const str = eval('(' + response.data.body + ')');
								console.log(str.id)
								//调用后端接口成功，得到sessionId，页面会在函数里面进行跳转
								return stripe.redirectToCheckout({ sessionId: str.id });
				    }).then(function (session) {
								console.log(session)
				    }).then(function (result) {
				        if (result.error) {
				            alert(result.error.message);
				        }
				    }).catch(function (error) {
				        console.log(error);
								console.log('失败')
				    });
			},
			cancel(){
				console.log('点击了取消')
				this.$emit('dialogVisibleEvent', false);
			}
		}
	}
</script>

<style>
	#mask-layer {
		width: 100%;
		height: 100%;
		background: rgba(204,204,204,.7);
		position: absolute;
		top: 0;
	}
	#checkout-button {
		
	}
</style>
