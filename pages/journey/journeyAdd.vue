<template>
    <view>
        <view class="tj-sction">
            <view class="tl-item">
                <text @tap="goToRetinueAdd">添加随员</text>
            </view>
            <view class="tr-item">
                <text @tap="deleteRetinue">删除选择随员</text>
            </view>
        </view>
        <!-- 列表 -->
        <view class="cart-list">
            <block v-for="(item, index) in cartList" :key="item.id">
                <view class="cart-item">
                    <view class="item-right">
                         <text><checkbox :value="item.value" :checked="item.checked" /></text>
                        <text class="item" v-if="false">{{item.id}}</text>
                        <text class="item">{{item.name}}</text>
                        <text class="item">{{item.phone}}</text>
                    </view>
                </view>
            </block>
        </view>
    </view>
</template>

<script>
    export default {

        data(){
            return {
				cartList:[],
                // cartList: [{
                //     id:'1',
                //     name:'张三',
                //     phone:'1735013423423'
                // },{
                //     id:'2',
                //     name:'张三',
                //     phone:'1735013423423'
                // },{
                //     id:'3',
                //     name:'张三',
                //     phone:'1735013423423'
                // }],
            }
        },

		onLoad(){
			this.getPatientinfo()
		},

		onNavigationBarButtonTap(e) {
			const index = e.index;
			if (index === 0) {
                 uni.reLaunch({
                     url: '/pages/journey/journey',
                 });
				console.log("test0")
			}else if(index === 1){
				const requestTask = uni.request({
				    url: 'http://127.0.0.1:2009/app/medical/patientinfo-save',
					method: 'POST',
				    data: {
				        name: 'name',
				        age: 18
				    },
				    success: function(res) {
				        console.log(res.data);
				    }
				});
				console.log("test1")
			}
		},

        methods: {
			deleteRetinue(){
				const requestTask = uni.request({
				    url: 'http://127.0.0.1:2009/app/medical/patientinfo-delete-detail',
					method: 'POST',
				    data: {
				        name: 'name',
				        age: 18
				    },
				    success: function(res) {
				        console.log(res.data);
				    }
				});
				
			},
			getPatientinfo(){
				const requestTask = uni.request({
				    url: 'http://127.0.0.1:2009/app/medical/patientinfo-page',
					method: 'POST',
				    data: {
				        name: 'name',
				        age: 18
				    },
				    success: function(res) {
				        console.log(res.data);
						this.cartList =res.data
				    }
				});
			},
            goToRetinueAdd(){
                console.log("console log")
                uni.reLaunch({
                    url: '../retinue/retinueAdd',
                });
            }

        }
    }
</script>

<style lang='scss'>
    .tj-sction{
        border-style:solid;
        border-width:1px;
        display: flex;
        align-items: center;
        /*padding: 34px 36px 16px 88px;*/
        /*line-height:50px;*/
        position: relative;
        .tl-item{
            flex: 1;
            width:185px;
            padding :10px 10px 10px 40px;
            /*font-size: 17px;*/
            color: #606266;
        }
        .tr-item{
            flex: 1;
            width:185px;
            /*font-size:17px;*/
            color: #606266;
        }
    }
    .cart-list{
        border-style:solid;
        border-width:1px;
        .cart-item{
            /*padding:10px 10px 10px 10px;*/
            .item-right{
                /*padding:40px 10px 10px 10px;*/
                .item{
                    padding :10px 10px 10px 40px;
                }
            }
        }

    }

</style>
