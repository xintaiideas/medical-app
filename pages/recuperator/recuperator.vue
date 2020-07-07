<template>
   <view>
	    <view class="yt-list-cell">
	    	<text class="cell-tit">用户:</text>
			<input class="desc" type="text" v-model="patientinfo.userId" placeholder="请输入用户" placeholder-class="placeholder" />
	    </view>
	    <view class="yt-list-cell">
	    	<text class="cell-tit ">联系电话:</text>
			<input class="desc" type="text" v-model="patientinfo.tel" placeholder="请输入联系电话" placeholder-class="placeholder" />
	    </view>
	    <view class="yt-list-cell">
	    	<text class="cell-tit ">姓名:</text>
			<input class="desc" type="text" v-model="patientinfo.name" placeholder="请输入姓名" placeholder-class="placeholder" />
	    </view>
	    <view class="yt-list-cell ">
	    	<text class="cell-tit ">性别:</text>
	    	<input class="desc" type="text" v-model="patientinfo.sex" placeholder="选择性别" placeholder-class="placeholder" />
	    </view>
		<view class="yt-list-cell ">
			<text class="cell-tit ">民族</text>
			<input class="desc" type="text" v-model="patientinfo.nation" placeholder="民族" placeholder-class="placeholder" />
		</view>
		<view class="yt-list-cell ">
			<text class="cell-tit ">婚姻状态</text>
			<input class="desc" type="text" v-model="patientinfo.marital" placeholder="婚姻状态" placeholder-class="placeholder" />
		</view>
		<view class="yt-list-cell ">
			<text class="cell-tit ">出生日期</text>
			<input class="desc" type="text" v-model="patientinfo.birthday" placeholder="出生日期" placeholder-class="placeholder" />
		</view>
		<view class="yt-list-cell ">
			<text class="cell-tit ">籍贯</text>
			<input class="desc" type="text" v-model="patientinfo.nativeId" placeholder="籍贯" placeholder-class="placeholder" />
		</view>
		<view class="yt-list-cell ">
			<text class="cell-tit ">入伍日期</text>
			<input class="desc" type="text" v-model="patientinfo.soldierInfo.militaryTime" placeholder="入伍日期" placeholder-class="placeholder" />
		</view>
		<view class="yt-list-cell ">
			<text class="cell-tit ">军官证号</text>
			<input class="desc" type="text" v-model="patientinfo.soldierInfo.militaryId" placeholder="军官证号" placeholder-class="placeholder" />
		</view>
		<view class="yt-list-cell ">
			<text class="cell-tit ">单位</text>
			<input class="desc" type="text" v-model="patientinfo.soldierInfo.dept" placeholder="单位" placeholder-class="placeholder" />
		</view>
		<view class="yt-list-cell ">
			<text class="cell-tit ">职务</text>
			<input class="desc" type="text" v-model="patientinfo.soldierInfo.post" placeholder="请输入职务" placeholder-class="placeholder" />
		</view>
		<view class="yt-list-cell ">
			<text class="cell-tit ">职级</text>
			<input class="desc" type="text" v-model="patientinfo.soldierInfo.postClass" placeholder="职级" placeholder-class="placeholder" />
		</view>
		<view class="yt-list-cell ">
			<text class="cell-tit ">衔级</text>
			<input class="desc" type="text" v-model="patientinfo.soldierInfo.militaryRank" placeholder="衔级" placeholder-class="placeholder" />
		</view>
		<view class="yt-list-cell ">
			<text class="cell-tit ">收缩压</text>
			<input class="desc" type="text" v-model="patientinfo.patientDynamicDetect.highBloodPressure" placeholder="收缩压" placeholder-class="placeholder" />
		</view>
		<view class="yt-list-cell ">
			<text class="cell-tit ">舒张压</text>
			<input class="desc" type="text" v-model="patientinfo.patientDynamicDetect.lowBloodPressure" placeholder="舒张压" placeholder-class="placeholder" />
		</view>
		<view class="yt-list-cell ">
			<text class="cell-tit ">体重(kg)</text>
			<input class="desc" type="text" v-model="patientinfo.patientDynamicDetect.weight" placeholder="体重(kg)" placeholder-class="placeholder" />
		</view>
		<view class="yt-list-cell ">
			<text class="cell-tit ">药物过敏</text>
			<input class="desc" type="text" v-model="patientinfo.patientDynamicDetect.drugAllergy" placeholder="药物过敏" placeholder-class="placeholder" />
		</view>
		<view class="yt-list-cell ">
			<text class="cell-tit ">病史及常用药</text>
			<input class="desc" type="text" v-model="patientinfo.patientDynamicDetect.medicalHistory" placeholder="病史及常用药" placeholder-class="placeholder" />
		</view>
	     <!-- 列表 -->
	    <!-- <view class="cart-list">
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
	   </view> -->
	    <view>
		   <button class="mini-btn" type="default" size="large" @tap="saveRecuperator">保存</button>
	   </view>
   </view>
</template>

<script>
    export default {
        data() {
            return {
                patientinfo: {
                       id: '',
                       userId: '',
                       parentId: '',
                       name: '',
                       sex: 1,
                       birthday: '',
                       medicareType: '',
                       cardNo: '',
                       nation: '',
                       idType: '',
                       idNo: '',
                       insuranceNum: '',
                       marital: 0,
                       nativeId: '',
                       address: '',
                       zipCode: '',
                       tel: '',
                       soldierInfo: {
                         patientId: '',
                         cnSpell: '',
                         militaryTime: '',
                         militaryId: '',
                         militaryInsuranceNum: '',
                         militaryBranch: '',
                         soldierType: '',
                         postStatus: '',
                         post: '',
                         postClass: '',
                         militaryRank: '',
                         dept: '',
                         bigDept: '',
                         zipCode: '',
                         deptAddress: '',
                         deptTel: '',
                         attachNum: '',
                         isSecretService: '',
                         secretService: '',
                         secretServiceType: '',
                         serviceStartTime: '',
                         serviceTotalTime: '',
                         remark: '',
                         createTime: '',
                         status: ''
                       },
                       patientDynamicDetect: {
                         id: '',
                         patientId: '',
                         stature: '',
                         weight: 0,
                         waistline: '',
                         hipline: '',
                         bloodType: '',
                         limosisBloodSugar: '',
                         afterMealBloodSugar: '',
                         temperature: '',
                         breathe: '',
                         pulse: '',
                         heartRate: '',
                         highBloodPressure: 0,
                         lowBloodPressure: 0,
                         geneticDisease: '',
                         medicalHistory: '',
                         primaryDiagnosis: '',
                         drugAllergy: '',
                         recordTime: ''
                       }
                     },
                cartList: [{
                    id:'1',
                    name:'张三',
                    phone:'1735013423423'
				},{
                    id:'2',
                    name:'张三',
                    phone:'1735013423423'
				},{
                    id:'3',
                    name:'张三',
                    phone:'1735013423423'
				}],
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
					    url: 'https://www.baidu.com',
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
            saveRecuperator(){
                uni.request({
                    url: 'http://127.0.0.1:2009/app/medical/patientinfo-save-detail', //仅为示例，并非真实接口地址。
					method: 'POST',
                    data:this.patientinfo,
                    header: {
                    	'content-type': 'application/x-www-form-urlencoded' //自定义请求头信息
                    },
                    success: (res) => {
                        console.log(res.data);
                    }
                });
				console.log("hello world")
			},
            goToJourneyAdd(){
                uni.reLaunch({
                    url: '../journey/journeyAdd',
                });
			},
            switch1Change: function (e) {
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


