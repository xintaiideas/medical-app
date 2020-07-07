<template>
	<view class="content">
		<view v-if="hasLogin" class="hello">
			<view class="title">
				您好 {{userName}}，您已成功登录。
			</view>
			<view class="ul">
				<view>这是 uni-app 带登录模板的示例App首页。</view>
				<view>在 “我的” 中点击 “退出” 可以 “注销当前账户”</view>
			</view>
		</view>
		<view v-if="!hasLogin" class="hello">
			<div>
				<div>
					<div class="slider-item">
						<a href="javascript:;">
							<div class="login-bg">
								<img src="../../static/img/header.png" alt="">
							</div>
						</a>
					</div>
					<!-- 分类 -->
					<view class="cate-section">
						<view class="cate-item">
							<image src="../../static/img/informationCollection@2x.png" data-rjs="2"></image>
							<text>信息采集</text>
						</view>
						<view class="cate-item">
							<image src="../../static/img/appointmentManagement@2x.png"></image>
							<text>预约管理</text>
						</view>
						<view class="cate-item">
							<image src="../../static/img/personnelManagement@2x.png"></image>
							<text>人员管理</text>
						</view>
						<view class="cate-item">
							<image src="../../static/img/therapyManagement@2x.png" @tap="bindRecuperationOne"></image>
							<text @tap="bindRecuperationOne">理疗管理</text>
						</view>
					</view>
					<view class="cate-section">
						<view class="cate-item">
							<image src="../../static/img/physicalManagement@2x.png"></image>
							<text>体检管理</text>
						</view>
						<view class="cate-item">
							<image src="../../static/img/recipeManagement@2x.png"></image>
							<text>食谱管理</text>
						</view>
						<view class="cate-item">
							<image src="../../static/img/trainingManagement@2x.png"></image>
							<text>体训管理</text>
						</view>
						<view class="cate-item">
							<image src="../../static/img/nursingManagement@2x.png"></image>
							<text>护理管理</text>
						</view>
					</view>
					<view class="cate-section">
						<view class="cate-item">
							<image src="../../static/img/medicationManagement@2x.png"></image>
							<text>用药管理</text>
						</view>
						<view class="cate-item">
							<image src="../../static/img/braceletConfiguration@2x.png"></image>
							<text>手环配置</text>
						</view>
						<view class="cate-item">
							<image src="../../static/img/Planmanagement@2x.png"></image>
							<text>计划管理</text>
						</view>
						<view class="cate-item">
							<image src="../../static/img/Dispatching@2x.png"></image>
							<text>派车管理</text>
						</view>
					</view>
					<div class="divHeight"></div>
					<!-- 猜你喜欢 -->
					<view class="f-header m-t">
						<image src="../../static/img/icon3_tj@2x.png" style="width:30px;height:30px"></image>
						<view class="tit-box">
							<text class="tit">重点关注</text>
						</view>
						<text class="yticon icon-you"></text>
						<div class="aui-arrow">
							更多<span></span>
						</div>
					</view>
				</div>
				<div class="aui-list-card">
					<a href="javascript:;" class="aui-flex b-line">
						<div class="aui-flex-box">
							<h3>张霄云</h3>
							<p>军衔：少将&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;职务：师长</p>
							<p>单位：东部战区46师</p>
							<p>时间：2019年9月16日&nbsp;&nbsp;人数：6个</p>
							<p>预约项目：理疗、体检、体训</p>
						</div>
						<view class="aui-card-img">
							<image src="../../static/img/zhangshaoyun.png" alt="" class="image"></image>
						</view>
					</a>
					<a href="javascript:;" class="aui-flex b-line">
						<div class="aui-flex-box">
							<h3>蔡文强</h3>
							<p>军衔：参谋长&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;职务：师长</p>
							<p>单位：野战部队东部战区16区68排</p>
							<p>时间：2019年9月16日&nbsp;人数：6个</p>
						</div>
						<view class="aui-card-img">
							<image src="../../static/img/caiwenqiang.png" alt="" class="image"></image>
						</view>
					</a>
					<a href="javascript:;" class="aui-flex b-line">
						<div class="aui-flex-box">
							<h3>谢建国</h3>
							<p>军衔：副参谋长&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;职务：师长</p>
							<p>单位：野战部队东部战区16区68排</p>
							<p>时间：2019年9月16日&nbsp;人数：6个</p>
						</div>
						<view class="aui-card-img">
							<image src="../../static/img/xiejianguo.png" alt="" class="image"></image>
						</view>
					</a>
				</div>
				<div class="pullUp">
					<span>已经没有更多啦！点击返回顶部 ↑</span>
				</div>
			</div>
		</view>
	</view>
</template>

<script>
	import '../../static/css/common.css'
	import '../../static/css/common.scss'
	import {
		mapState
	} from 'vuex'
	

	export default {
		data() {
			return {
				isActive: false,
			}
		},
		computed: mapState(['forcedLogin', 'hasLogin', 'userName']),
		onLoad() {
			if (this.hasLogin) {
				uni.showModal({
					title: '未登录',
					content: '您未登录，需要登录后才能继续',
					/**
					 * 如果需要强制登录，不显示取消按钮
					 */
					showCancel: !this.forcedLogin,
					success: (res) => {
						if (res.confirm) {
							/**
							 * 如果需要强制登录，使用reLaunch方式
							 */
							if (this.forcedLogin) {
								uni.reLaunch({
									url: '../login/login'
								});
							} else {
								uni.navigateTo({
									url: '../login/login'
								});
							}
						}
					}
				});
			}
		},
		methods: {
			activityManager() {
				if (this.isActive) {
					document.getElementById("activity").src = "../../static/img/nursingManagement@2x.png";
					this.isActive = false;
				} else {
					document.getElementById("activity").src = "../../static/img/trainingManagement@2x.png";
					this.isActive = true;
				}
			},
			fun() {

				if (this.isActive) {
					document.getElementById("img").src = "../../static/img/nursingManagement@2x.png";
					this.isActive = false;
				} else {
					document.getElementById("img").src = "../../static/img/nursingManagement@2x_gaolian.png";
					this.isActive = true;
				}
				console.log('您好，我叫详情');
			},
			bindLogin() {
				uni.reLaunch({
					url: '../user/user',
				});
			},
			bindLogout() {
				this.logout();
				/**
				 * 如果需要强制登录跳转回登录页面
				 */
				if (this.forcedLogin) {
					uni.reLaunch({
						url: '../login/login',
					});
				}
			},
			bindRecuperation() {
				uni.reLaunch({
					url: '../scenery/scenery',
				});
			},
			bindRecuperationOne() {
				uni.reLaunch({
					url: '../scenery/sceneryOne',
				});
			},
		}
	}
</script>
<style>
	.active {
		background-color: #ffdfe1;
		border-radius: 30%;
	}
</style>