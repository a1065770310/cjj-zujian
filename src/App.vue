<template>
	<div id="app">
		<fenye ref="child" :value="value">
			<div slot="prev">
				<button class="btn" @click="prev"> - </button>
			</div>
			<div slot="next">
				<button class="btn" @click="next"> +</button>
			</div>
			<div slot="jump">
				<input type="text"   class="jump" v-model="value"/>
				<button class="jumpBtn" @click="jump">跳转</button>
			</div>
		</fenye>
		<router-view />
		
	</div>
</template>
<script>
	import fenye from './components/page.vue'
	export default {
		name: 'App',
		data(){
			return{
				value:''
			}
		},
		components: {
			fenye:fenye
		},
		methods:{
			prev(){
				this.$refs.child.prev()
			},
			next(){
				this.$refs.child.next()
			},
			jump(){
				this.$refs.child.jump()
				
			}
		}
	}
	

</script>

<style scoped="scoped">
</style>
