<template>
    <view>
        <view>
            基本信息(必须填写)
        </view>
        <view class="tj-sction">
            <text class="tl-item" style="padding-bottom:105px"> 证件类型</text>
            <view class="tr-item">
                <checkbox-group >
                    <label class="aui-arrow" >
                        <checkbox value="china" checked="true" />中国居民身份证
                    </label>
                    <label class="aui-arrow">
                        <checkbox value="foreign" />外国人永久居留身份证
                    </label>
                    <label class="aui-arrow">
                        <checkbox value="hongkong" />港澳台居民居住证
                    </label>
                </checkbox-group>
            </view>
        </view>
        <view class="tj-sction">
            <text class="tl-item">姓名</text>
            <input class="tr-item" type="text" v-model="username" placeholder="姓名" placeholder-class="placeholder" />
        </view>
        <view class="tj-sction">
            <text class="tl-item">性别</text>
            <checkbox-group class="tr-item">
                <label>
                    <checkbox value="sex" checked="true" />男
                </label>
                <label>
                    <checkbox value="sex" />女
                </label>
            </checkbox-group>
        </view>
        <view class="tj-sction">
            <text class="tl-item">民族</text>
            <input class="tr-item" type="text" v-model="nation" placeholder="民族" placeholder-class="placeholder" />
        </view>
        <view class="tj-sction">
            <text class="tl-item">籍贯</text>
            <input class="tr-item" type="text" v-model="nativePlace" placeholder="籍贯" placeholder-class="placeholder" />
        </view>
        <view class="tj-sction">
            <text class="tl-item">身份证号</text>
            <input class="tr-item" type="text" v-model="idNumber" placeholder="身份证号" placeholder-class="placeholder" />
        </view>
        <view class="tj-sction">
            <text class="tl-item">联系方式</text>
            <input class="tr-item" type="text" v-model="contact" placeholder="联系方式" placeholder-class="placeholder" />
        </view>
    </view>
</template>

<script>
    export default {

        data(){
            return {
                china:false,
                foreign:false,
                hongkong:false,
                username:'',
                sex:'',
                nation:'',
                nativePlace:'',
                idNumber:'',
                contact:''
            }
        },
		onNavigationBarButtonTap(e) {
			const index = e.index;
			if (index === 0) {
                 uni.reLaunch({
                     url: '/pages/journey/journeyAdd',
                 });
				console.log("test0")
			}else if(index === 1){
				const requestTask = uni.request({
				    url: 'http://127.0.0.1:2009/app/medical/patientinfo-save-detail',
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

        }
    }
</script>

<style lang='scss'>
    .tj-sction{
        display: flex;
        align-items: center;
        /*padding: 34px 36px 16px 88px;*/
        line-height:50px;
        /*position: relative;*/
        .tl-item{
            flex: 1;
            color: #606266;
        }
        .tr-item{
            border-style:solid;
            border-width:1px;
            flex: 2;
            color: #606266;
            .aui-arrow{
                display: inline-block;
                vertical-align: middle;
            }
        }
    }
</style>
