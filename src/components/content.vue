<template>
  <div id="content">
	<div class="list">
		<div class="avatar">
			<img  width='32px' height='32px' src="" alt="avatar">
		</div>
		<div class="list-content">
			<div class="list-title">
				<span class="name">RO1班</span>
				<span class="city">1人|北京</span>
			</div>
			<div class="tag">
				<ul>
					<li>标签1</li>
					<li>标签2</li>
					<li>标签3</li>
				</ul>
			</div>
			<div class="describe" v-show="!this.tipsShow">
				<ul>
					<li>3km</li>
					<li>1元1天</li>
					<li>10元/天</li>
					<li>最少一周</li>
				</ul>
				<span class="detailed" @click="showTips">
					>
				</span>
			</div>
			<div class="describe-more" v-show="this.tipsShow">
				<div class="describe-tag">
					<ul>
						<li>3km</li>
						<li>1周1天</li>
						<li>10元/天</li>
						<li>最少一周</li>
					</ul>
				</div>
				<div class="describe-con">
					<ul>
						<li>每次跑不低于3公里</li>
						<li>每周跑1天</li>
						<li>每天契约金10元</li>
						<li>至少参加一周</li>
					</ul>
				</div>
				<span class="detailed" @click="showTips">
					?
				</span>
			</div>
		</div>
	</div>
  </div>
</template>

<script>
	export default {
		data() {
			return{
				tipsShow: false
			}
		},
		created() {
	        this.$http.get('/api/classes').then((response) =>{
	          response = response.body;
	          console.log(response);
	          this.classes = response.data;
	          console.log(this.classes);
	        })
	    },
	    methods: {
			showTips() {
				this.tipsShow = !this.tipsShow;
			}
	    }
	}
</script>

<style scoped>
	.list{
		padding: 10px 0;
		display: flex;
		border-bottom: 1px solid #000;
	}
	.avatar{
		display: inline-block;
		padding: 15px 30px 15px 0;
	}
	.list-content{
		display: inline-block;
		/*padding-top: 15px;*/
		font-size: 12px;
		flex: 1;

	}
	.list-title{
		height: 30px;
		line-height: 30px;
		overflow: hidden;
	}
	.name{
		float: left;
	}
	.city{
		float: right;
		margin-right: 15px;
	}
	.tag{
		height: 30px;
		line-height: 30px;
		font-size: 12px;

	}
	.tag li{
		display: inline-block;
	}
	.describe{
		margin-top: 5px;
		height: 25px;
		line-height: 25px;
		/*display: none;*/
	}
	.describe ul{
		display: inline-block;
	}
	.describe ul li{
		display: inline-block;
		background-color: pink;
		color: #fff;
		border-radius: 2px;
		padding: 0 4px;
		font-size: 4px;
		margin: auto 0;
	}
	.detailed{
		/*width: 25px;*/
		height: 25px;
		line-height: 25px;
		margin-left: 20px;

	}
	.describe-tag{
		float: left;
	}
	.describe-con{
		float: left;
	}
	.describe-more li{
	    margin-bottom: 10px;
	}
	.describe-tag li{
		background-color: pink;
		color: #fff;
		border-radius: 2px;
		padding: 0 4px;
		font-size: 4px;
		width: auto;
	}
</style>