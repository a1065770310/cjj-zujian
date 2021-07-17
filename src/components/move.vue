<template>
	<div id="move">
		<div class="left">
			<input @click="checkAll1" :disabled="leftDisabled" type="checkbox" class="checkAll" :checked="checkAllLeft" />
			<span v-if="current>0">{{current}}/</span>
			<span>{{leftList.length}}</span>
			<div class="list">
				<div class="queryBox" :class="{present:borderLeft==true}">
					<input type="text" @keyup="shuru" class="query" @focus="huoqu" @blur="shiqu" placeholder="请输入搜索内容" v-model="value" />
				</div>
				<ul class="leftList">
					<li @click="leftdianji(index)" v-for="(item,index) in leftList" :key="index">
						<input type="checkbox" :checked="item.check" :disabled="item.disabled" />{{item.text}}
					</li>
				</ul>
			</div>
		</div>
		<div class="btnBox">
			<button class="moveRight" @click="moveRight">右移</button>
			<button class="moveLeft" @click="moveLeft">左移</button>
		</div>
		<div class="right">
			<input @click="checkAll2" :disabled="rightDisabled" type="checkbox" class="checkAll" :checked="checkAllRight" />
			<span v-if="current2>0">{{current2}}/</span>
			<span>{{rightList.length}}</span>
			<div class="list">
				<div class="queryBox" :class="{present2:borderLeft2==true}">
					<input type="text" @keyup="shuru" class="query" @focus="huoqu2" @blur="shiqu2" placeholder="请输入搜索内容" v-model="value" />
				</div>
				<ul class="rightList">
					<li @click="rightdianji(index)" v-for="(item,index) in rightList" :key="index">
						<input type="checkbox" :checked="item.check" :disabled="item.disabled"/>{{item.text}}
					</li>
				</ul>
			</div>
		</div>
		<van-switch v-model="checked" @click="ev_disabled"></van-switch>
	</div>
</template>

<script>
	export default {
		name: 'move',
		data() {
			return {
				borderLeft: false,
				borderLeft2: false,
				checkAllLeft: false,
				checkAllRight: false,
				disabled: true,
				leftDisabled:false,
				rightDisabled:false,
				current: '',
				current2: '',
				value: '',
				checked: true,
				leftList: [{
						disabled: false,
						text: '小红',
						check: false,
						change: true
					},
					{
						disabled: false,
						text: '小橙',
						check: false,
						change: true
					},
					{
						disabled: true,
						text: '小黄',
						check: false,
						change: false
					},
					{
						disabled: true,
						text: '小绿',
						check: false,
						change: false
					},
					{
						disabled: true,
						text: '小青',
						check: false,
						change: false
					},
					{
						disabled: false,
						text: '小蓝',
						check: false,
						change: true
					},
					{
						disabled: false,
						text: '小白',
						check: false,
						change: true
					},
					{
						disabled: false,
						text: '小黑',
						check: false,
						change: true
					}
				],
				rightList: [{
						disabled: false,
						text: '大红',
						check: false,
						change: true
					},
					{
						disabled: false,
						text: '大橙',
						check: false,
						change: true
					},
					{
						disabled: false,
						text: '大蓝',
						check: false,
						change: true
					},
					{
						disabled: false,
						text: '大白',
						check: false,
						change: true
					},
					{
						disabled: false,
						text: '大黑',
						check: false,
						change: true
					}
				]
			}
		},
		methods: {
			leftdianji(index) {
				var arr3 = []
				if (this.leftList[index].disabled == false) {
					this.leftList[index].check = !this.leftList[index].check
				}

				this.leftList.forEach(item => {
					if (item.check == true) {
						arr3.push(item)
						this.current = arr3.length

					}
					if (arr3.length == 0) {
						this.current = 0
					}
				})
			},
			rightdianji(index) {
				var arr4 = []
				this.rightList[index].check = !this.rightList[index].check
				this.rightList.forEach(item => {
					if (item.check == true) {
						arr4.push(item)
						this.current2 = arr4.length
						console.log(arr4.length)
					}
					if (arr4.length == 0) {
						this.current2 = 0
					}
				})
			},
			moveRight() {
				var arr = []
				this.current = 0
				this.leftList.forEach(item => {
					if (item.check == true) {
						item.check = false
						// delete item.check
						arr.push(item)
					}
					console.log(item)
				})
				this.checkAllLeft = false
				arr.forEach(item => {
					var idx = this.leftList.indexOf(item)
					this.leftList.splice(idx, 1)
				})
				this.rightList.push(...arr)

			},
			moveLeft() {
				var arr2 = []
				this.current2 = 0
				this.rightList.forEach(item => {
					if (item.check == true) {
						item.check = false
						arr2.push(item)
					}
				})
				this.checkAllRight = false
				arr2.forEach(item => {
					var idx = this.rightList.indexOf(item)
					this.rightList.splice(idx, 1)
				})
				this.leftList.push(...arr2)

			},
			checkAll1() {
				this.checkAllLeft = !this.checkAllLeft
				var flag = true
				var arr3 = []
				this.leftList.forEach(item => {
					if (item.check == false && item.disabled == false) {
						flag = false
					}
				})
				this.leftList.forEach(item => {
					if (flag == false && item.disabled == false) {
						item.check = true
						arr3.push(item)
						this.current = arr3.length
					} else {
						item.check = false
						this.current = 0
					}
				})

			},
			checkAll2() {
				this.checkAllRight = !this.checkAllRight
				var flag = true
				var arr4 = []
				this.rightList.forEach(item => {
					if (item.check == false) {
						flag = false
					}
				})
				this.rightList.forEach(item => {
					if (flag == false) {
						item.check = true
						arr4.push(item)
						this.current2 = arr4.length
					} else {
						item.check = false
						this.current2 = 0
					}
				})
			},
			huoqu() {
				this.borderLeft = true

			},
			shiqu() {
				this.borderLeft = false
			},
			huoqu2() {
				this.borderLeft2 = true

			},
			shiqu2() {
				this.borderLeft2 = false
			},
			shuru() {

			},
			ev_disabled() {
				if (this.checked == true) {
					this.leftList.forEach(item => {
						if (item.disabled == false && item.change == true) {
							item.disabled = true
						}
					})
					this.rightList.forEach(item => {
						if (item.disabled == false && item.change == true) {
							item.disabled = true
						}
					})
					this.leftDisabled=true
					this.rightDisabled=true
					console.log(this.checked)
				}else{
					this.leftList.forEach(item => {
						if (item.disabled == true && item.change == true) {
							item.disabled = false
						}
					})
					this.rightList.forEach(item => {
						if (item.disabled == true && item.change == true) {
							item.disabled = false
						}
					})
					this.leftDisabled=false
					this.rightDisabled=false
				}

			},

		},
		mounted() {

		}
	}
</script>

<style scoped="scoped">
	#move {
		display: flex;
	}

	ul,
	li {
		list-style: none;
		margin: 0;
		padding: 0;
	}

	.list {
		border-top: 1px solid beige;
	}

	ul {

		height: 100px;

		overflow-y: scroll;
	}

	li {
		display: flex;
		justify-content: space-between;
	}

	.queryBox {
		width: 100px;
		height: 20px;
		margin: 10px;
		border: 1px solid bisque;
		position: relative;
	}

	.query {
		width: 80%;
		height: 19px;
		border: none;
		outline: none;
		position: absolute;
		top: 50%;
		left: 50%;
		transform: translate(-50%, -50%);

	}

	.present {
		border: 1px solid #65dbfe;
	}

	.present2 {
		border: 1px solid #65dbfe;
	}

	.btnBox {
		display: flex;
		flex-direction: column;
		margin: 0 0 0 50px;
		justify-content: space-between;
	}

	button {
		width: 50px;
		height: 25px;
	}

	.left {
		margin-left: 50px;
		border: 1px solid beige;
	}

	.right {
		margin-left: 50px;
		border: 1px solid beige;
	}
</style>
