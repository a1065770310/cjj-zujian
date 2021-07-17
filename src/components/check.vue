<template>
	<div id="check">
		<ul>
			<li v-for="(item,index) in checkList" :key="index">
				<span @click="check(index)" :class="{present:item.check==true}"></span>
			</li>
		</ul>
		<span class="checkAll" @click="checkAll"></span>全选
	</div>
</template>

<script>
	export default{
		name:"check",
		
		data(){
			return{
				checkList:[
					{
						check:false
					},
					{
						check:false
					},
					{
						check:false
					},
					{
						check:false
					}
				]
			}
		},
		methods:{
			check(index){
				this.checkList[index].check=!this.checkList[index].check
				console.log(this.checkList[index].check)
			},
			checkAll(){
				var flag=true
				this.checkList.forEach(item =>{
					if(item.check==false){
						flag=false
						console.log('1',flag)
					}
					
				})
				this.checkList.forEach(item =>{
					if(flag==false){
						item.check=true
					}else{
						item.check=false	
					}
				})
			}
		}
	}
</script>

<style scoped="scoped">
	ul,li{
		list-style: none;
	}
	ul li{
		margin-top: 0.2rem;
	}
	ul li span{
		display: inline-block;
		width: 0.5rem;
		height: 0.5rem;
		border-radius: 50%;
		background-color: #FF0000;
	}
	.checkAll{
		display: inline-block;
		width: 0.5rem;
		height: 0.5rem;
		border-radius: 50%;
		background-color: #FF0000;
	}
	.present{
		background-color: black;
	}
</style>
