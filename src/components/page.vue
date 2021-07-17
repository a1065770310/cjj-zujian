<template>
	<div id="page">
		<slot name="prev"></slot>
		<!-- <button class="btn" @click="prev"> - </button> -->
		<ul>
			<li :class="{present:current==idx}" v-for="(item,idx) in page" :key="idx" @click="ev_click(idx)">{{item}}</li>
		</ul>
		
		<slot name="next"></slot>
		<!-- <button class="btn" @click="next"> +</button> -->
		<slot name="jump"></slot>
		<!-- <input type="text"  class="jump" v-model="value"/> -->
		<!-- <button class="jumpBtn" @click="jump">跳转</button> -->
	</div>
</template>

<script>
	export default{
		name:"page",
		data(){
			return{
				current:0,
				page:10,
				
			}
		},
		props:{
			value:String
		},
		mounted(){
			
		},
		methods:{
			ev_click(idx) {
				this.current=idx
				
			},
			prev(){
				if(this.current>0){
					this.current=parseInt(this.current-1)
				}else{
					this.current=0
				}
			},
			next(){
				if(this.current<this.page-1){
					this.current=parseInt(this.current+1)
				}else{
					this.current=9
				}
			},
			jump(){
				this.current=parseInt(this.value)-1
			}
		}
	}
		
</script>

<style scoped="scoped">
	#page{
		display: flex;
	}
	ul {
		display: flex;
	}

	li {
		width: 30px;
		height: 30px;
		text-align: center;
		line-height: 30px;
		border: 1px solid #646566;
		margin-left: 10px;
	}
	.present{
		background-color: #0570DB;
	}
	.btn{
		width: 30px;
		height: 30px;
		margin-left: 10px;
		font-size: 5px;
	}
	.jump{
		margin-left: 10px;
		width: 30px;
	}
	.jumpBtn{
		height: 30px;
		margin-left: 10px;
		font-size: 5px;
	}
</style>
