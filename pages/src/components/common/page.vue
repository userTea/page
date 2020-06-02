<template>
	<div>
		<ul>
			<li @click="goPage(-1)">上一页</li>
			<li v-for="page in showPageBtn" :class="{'active':page == curPage}">
				<span @click="goPage(0, page)">{{page || '...'}}</span>
			</li>
			<li @click="goPage(1)">下一页</li>
		</ul>
		<span class="skip">前往<input type="number" @keyup.enter="onSkip($event)">页</span>
	</div>
</template>

<script>
	export default {
		props: {
			pages: {
				type: Number,
				default: 1
			},
			current: {
				type: Number,
				default: 1
			}
		},
		data() {
			return {
				curPage: 1
			}
		},
		computed: {
			showPageBtn() {
				let pageNum = this.pages;
				let index = this.curPage;
				let arr = [];
				if (pageNum <= 5) {
					for (let i = 1; i <= pageNum; i++) {
						arr.push(i)
					}
					return arr
				}
				if (index <= 2) return [1, 2, 3, 0, pageNum];
				if (index >= pageNum - 1) return [1, 0, pageNum - 2, pageNum - 1, pageNum];
				if (index === 3) return [1, 2, 3, 4, 0, pageNum];
				if (index === pageNum - 2) return [1, 0, pageNum - 3, pageNum - 2, pageNum - 1, pageNum];
				return [1, 0, index - 1, index, index + 1, 0, pageNum];
			}
		},
		methods: {
			goPage(status, page) {
				if(status !== 0){
					//上一页或下一页
					if(status === -1 && this.curPage == 1) return;
					if(status === 1 && this.curPage == this.pages) return;
					
					this.curPage += status;
				}else{
					if(page < 1 || page > this.pages) return;
					if (this.curPage != page) {
						this.curPage = page;
					} else {
						console.log('Already in the current page');
						return;
					}
				}
				
				this.$emit('change', this.curPage);
			},
			onSkip(e){
				let value = e.target.value;
				if(!value || isNaN(value)){
					e.target.value = '';
				}
				this.goPage(0, parseInt(value));
			}
		}
	}
</script>

<style scoped>
	ul{
		display: inline-block;
		list-style: none;
		border-left: 1px solid #ccc;
		margin: 0;
		padding: 0;
	}
	li{
		display: inline-block;
		width: 40px;
		line-height: 40px;
		text-align: center;
		font-size: 12px;
		border: 1px solid #ccc;
		border-left: none;
		cursor: pointer;
	}
	li.active{
		color: #fff;
		background: #01AAED;
	}
	li span{
		display: block;
	}
	.skip{
		margin-left: 30px;
	}
	.skip input{
		text-align: center;
		width: 40px;
		height: 20px;
	}
</style>
