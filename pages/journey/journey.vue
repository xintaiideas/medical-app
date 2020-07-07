<template>
   <view>
	    <view class="yt-list-cell">
	    	<text class="cell-tit">疗养证号:</text>
			<input class="desc" type="text" v-model="cardNo" placeholder="请输入疗养证号" placeholder-class="placeholder" />
	    </view>
	    <view class="yt-list-cell">
	    	<text class="cell-tit ">姓名:</text>
			<input class="desc" type="text" v-model="name" placeholder="请输入姓名" placeholder-class="placeholder" />
	    </view>
	    <view class="yt-list-cell">
	    	<text class="cell-tit ">联系电话:</text>
			<input class="desc" type="text" v-model="tel" placeholder="请输入联系电话" placeholder-class="placeholder" />
	    </view>
	    <view class="yt-list-cell ">
	    	<text class="cell-tit ">启程时间:</text>
	    	<input class="desc" type="text" v-model="receiveTime" placeholder="选择启程时间" placeholder-class="placeholder" />
	    </view>
		<view class="yt-list-cell ">
			<text class="cell-tit ">航班号/车次</text>
			<input class="desc" type="text" v-model="trafficNo" placeholder="航班号/车次" placeholder-class="placeholder" />
		</view>
	    <view>
		   <view>
			   <switch size="mini" checked @change="switch1Change" />有随员
		   </view>
	   </view>
	     <!-- 列表 -->
	    <view class="cart-list" v-if="show==true">
		   <block v-for="(item, index) in cartList" :key="item.id">
			   <view
					   class="cart-item"
			   >
				   <view class="item-right">
					   <text class="item" v-if="false">{{item.id}}</text>
					   <text class="item">{{item.name}}</text>
					   <text class="item">{{item.phone}}</text>
					   <text class="item" @click="deleteCartItem(item.id)">删除</text>
				   </view>
			   </view>
		   </block>
	   </view>
	    <view >
		   <button class="mini-btn" type="default" size="large" @tap="goToJourneyAdd">增加随员</button>
	   </view>
   </view>
</template>

<script>
    export default {
        data() {
            return {
                cardNo:'',
                name:'',
                tel:'',
                receiveTime:'',
                trafficNo:'',
				cartList:[],
    //             cartList: [{
    //                 id:'1',
    //                 name:'张三',
    //                 phone:'1735013423423'
				// },{
    //                 id:'2',
    //                 name:'张三',
    //                 phone:'1735013423423'
				// },{
    //                 id:'3',
    //                 name:'张三',
    //                 phone:'1735013423423'
				// }],
            };
        },

		onNavigationBarButtonTap(e) {
			const index = e.index;
			if (index === 0) {
                 uni.switchTab({
                     url: '/pages/scenery/scenery',
                 });
				console.log("test0")
			}else if(index === 1){
				const requestTask = uni.request({
				    url: 'http://127.0.0.1:2009/app/medical/recuperation-save-detail',
					method: 'POST',
				    data: {
				     cardNo:this.cardNo,
					 name :this.name,
					 tel : this.tel,
					 receiveTime: this.receiveTime,
					 trafficNo:this.trafficNo,
					   
				    },
				    success: function(res) {
				        console.log(res.data);
				    }
				});
				console.log("test1")
			}
		},

		onLoad(){
			this.getInpatientrecord()
		},
        methods: {
			getInpatientrecord(){
				const requestTask = uni.request({
				    url: 'http://127.0.0.1:2009/app/medical/patientinfo-page',
					method: 'POST',
				    data: {"name":"","cardNo":"","idNo":"","insuranceNum":"","address":"","zipCode":"","tel":"","unit":"","profession":"","familyAddress":"","email":"","photo":"","guardian":"","guardianTel":"","secondGuardian":"","secondGuardianTel":"","remark":"","parentId":0,"start":0,"limit":10},
				    success: function(res) {
				        console.log(res.data);
						this.cartList = res.data
				    }
				});
			},
            goToJourneyAdd(){
                uni.reLaunch({
                    url: '../journey/journeyAdd',
                });
			},
            switch1Change: function (e) {
				
				this.show = e.target.value
                console.log('switch1 发生 change 事件，携带值为', e.target.value)
            },
            deleteCartItem(e){
                console.log('删除数据条操作')
			}
        }
    }
</script>
<style lang="scss">
	page {
		background: #ffffff;
	}
	.yt-list-cell {
		display: flex;
		align-items: center;
		/*padding: 34px 3px 16px 88px;*/
		line-height:55px;
		position: relative;
		.cell-tit {
			flex: 1;
			font-size: 22px;
			color: #606266;
		}
		.desc {
			flex: 2;
			font-size:22px;
			border-style:solid;
			border-width:1px;
			color: #606266;
		}
	}
	.cart-list{
		border-style:solid;
		border-width:1px;
		.cart-item{
			.item-right{
				padding :0px 4px 10px 0px;
               .item{
				   padding :10px 10px 10px 40px;
			   }
			}
		}
	}
</style>


