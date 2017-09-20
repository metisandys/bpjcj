<template>
  <div id="content">
	<div class="list" v-for="(item, index) in showList" :key="item.id">
		<div class="avatar">
			<img  width='32' height='32' :src="item.avatar" alt="avatar">
		</div>
		<div class="list-content">
			<div class="list-title">
				<span class="name">{{item.name}}</span>
				<span class="city">{{item.num}}人|{{item.city}}</span>
			</div>
			<div class="tag">
				<ul>
					<li v-for="text in newList[index]">{{text}}</li><!-- 
					<li>标签2</li>
					<li>标签3</li> -->
				</ul>
			</div>
			<div class="describe" v-show="!selected[item.id + '_flag']">
				<span>{{item.distance}}km</span>
				<span>1周{{item.required_duration}}天</span>
				<span>{{item.money / 100}}元/天</span>
				<span>最少{{item.limit_cycles}}周</span>
			</div>
			<div class="detailed" @click="showTips(item.id)" v-show="!selected[item.id + '_flag']">
				<img width="17" height="17" src="../assets/2.png" alt="">
			</div>
			<div class="describe-more" v-show="selected[item.id + '_flag']">
				<div class="tag-more">
					<ul>
						<li>
							<span class="describe-tag">{{item.distance}}km</span>
							<span class="describe-xx">每次跑不低于{{item.distance}}公里</span>
						</li>
						<li>
							<span class="describe-tag">1周{{item.required_duration}}天</span>
							<span class="describe-xx">每周跑{{item.required_duration}}天</span>
						</li>
						<li>
							<span class="describe-tag">{{item.money / 100}}元</span>
							<span class="describe-xx">每天契约金{{item.money / 100}}元</span>
						</li>
						<li>
							<span class="describe-tag">最少{{item.limit_cycles}}周</span><span class="describe-xx">至少参加{{item.limit_cycles}}周</span>
						</li>
					</ul>
				</div>
			</div>
			<div class="detailed" @click="showTips(item.id)" v-show="selected[item.id + '_flag']">
				<img width="17" height="17" src="../assets/1.png" alt="">
			</div>
		</div>
	</div>
	<div class="seeMore" @click="showMore = !showMore">查看更多></div>
  </div>

</template>

<script>
	export default {
		data() {
			return{
				classes: [],
				tipsShow: false,
				showMore: false,
				selected: []
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
		computed: {
			showList: function(){
				if(this.showMore == false){
					let showList = [];
					if(this.classes.length > 3){
						for(let i=0;i<3;i++){
							showList.push(this.classes[i]);
						}
					}else{
						showList = this.classes;
					}
					return showList;
				}else{
					return this.classes;
				}
    		},
    		newList: function(){
    			return this.classes.map(v => v.tags);
    		}
	    },
	    methods: {
			showTips: function(id) {
				if (!id) return
				let str = id + '_flag'
				if (this.selected.hasOwnProperty(str)) {
					this.selected[id + '_flag'] = !this.selected[id + '_flag']
				} else {
					this.$set(this.selected, str, true)
				}
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
	@media screen and (-webkit-min-device-pixel-ratio: 2) {
    	.list { border-bottom: 0.5px solid #000 }
	}
	@media screen and (-webkit-min-device-pixel-ratio: 3) {
    	.list { border-bottom: 0.333333px solid #000 }
	}
	.avatar{
		display: inline-block;
		padding: 15px 30px 15px 0;
	}
	.list-content{
		display: inline-block;
		font-size: 12px;
		flex: 1;
		position: relative;
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
		float: left;
		margin-right: 4px;
	}
	.describe{
		margin-top: 5px;
		line-height: 17px;
	}
	.describe span{
		float: left;
		background-color: pink;
		color: #fff;
		border-radius: 2px;
		padding: 0 4px;
		margin-right: 5px;
	}
	.detailed{
		position: absolute;
		right: 35px;
		top: 65px;
	}
	.describe-more{
		margin-top: 5px;
		position: relative;
	}
	.tag-more{
		display: inline-block;
	}
	.tag-more li{
	    line-height: 17px;
	    margin-bottom: 2px;
	}
	.describe-tag {
		display: inline;
		height: 17px;
		background-color: pink;
		color: #fff;
		border-radius: 2px;
		padding: 0 4px;
	}
	.describe-xx{
		position: absolute;
		left: 60px;
	}
	.seeMore{
		height: 30px;
		line-height: 30px;
		text-align: center;
	}
</style>