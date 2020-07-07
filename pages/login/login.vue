<template>
	<div class="login-page">
		<div class="login-bg">
			<div class="login-contain" style="position: absolute;">
				<img src="../../static/img/bg@2x.png" style="width: 100%;height: 270px;color: #ffffff;background-size: 35% 35%;no-repeat fixed;margin-top: -90px;">
				<div class="login-header">
					<img src="../../static/img/logo@2x.png" style="margin-top: -145px;margin-bottom: 0px;position: absolute;float: left;">
				</div>
				<div class="form-group">
					<div class="form-item">
						<label for="username">
							<img src="../../static/img/icon_iphone@2x.png">
						</label>
						<input id="username" type="text" v-model="username" placeholder="请输入您的手机号">
					</div>
					<div class="form-item">
						<label for="password">
							<img src="../../static/img/icon_password@2x.png" alt="">
						</label>
						<input id="password" type="password" v-model="password" placeholder="请输入您的密码">
					</div>
				</div>
				<div class="button-group">
					<button class="confirm-btn" @tap="bindLogin" >登录</button>
				</div>

				<div class="order-login">
					<p class="order-login-line">第三方账号登录</p>
					<div class="order-login-box">
						<view class="cate-section">
							<view class="cate-item">
								<image src="../../static/img/icon_weixin@2x.png"></image>
							</view>
							<view class="cate-item">
								<image src="../../static/img/icon_qq@2x.png"></image>
							</view>
							<view class="cate-item">
								<image src="../../static/img/icon_weibo@2x.png"></image>
							</view>
						</view>
					</div>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
	import {
		mapState,
		mapMutations
	} from 'vuex'
	export default {
		computed: {
			...mapState(['hasLogin', 'forcedLogin'])
		},
		data() {
			return {
				username: '',
				password: '',
			}
		},
		methods: {
			bindLogin() {
			 
				// uni.reLaunch({
				//     url: '../main/main',
				// });	
				uni.request({
					url: 'http://127.0.0.1:2009/app/account/login', //仅为示例，并非真实接口地址。
					// url: 'https://education.biandaozixishi.com/app/account/login', //仅为示例，并非真实接口地址。
					method: 'POST',
					data: {
						username: this.username,
						password: this.password,
						ip: '1.1.1.1',
					},
					header: {
						'content-type': 'application/x-www-form-urlencoded' //自定义请求头信息
					},
					success: (res) => {
						console.log(res.data.data.token)
						
						// let header = 'Bearer ' + res.data.data.token
					
						uni.request({
						    url: 'http://127.0.0.1:2009/app/medical/patientinfo-get-detail-byname', //仅为示例，并非真实接口地址。
							method: 'GET',
						    data: {
						        id: res.data.data.account.id,
						        username: res.data.data.account.username
						    },
							header: {
								'Authorization': 'Bearer ' + res.data.data.token, //自定义请求头信息
							},
						    success: function(res) {
								  // console.log(res.data.data.name+"------------------------------");
								// if(res.data.data==null){
								// 	uni.navigateTo({
								// 	    url: '/pages/recuperator/recuperator?id=1'
								// 	});
								// }else{
								// 	console.log("jia you shao nian")
								// }
						      
						    }
						});
					
						console.log(res.data.data.roles[0].name)
						if (res.data.data.roles[0].name == "管理员") {
							uni.reLaunch({
								url: '../main/main',
							});
						} else {
							uni.reLaunch({
								url: '../scenery/scenery',
							});
						}
					},


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
			}
		}
	}
</script>

<style scoped>
	/* login-page img{
		width: 100%;
		height: 500px;
		background: url(../../static/img/bg@2x.png) no-repeat fixed;
		color: #ffffff;
		background-size: 35% 35%;
		display: inline-block;
	} */
	body,
	html,
	div,
	a,
	span,
	p,
	h1,
	h2,
	h3,
	h4,
	h5,
	ul,
	li,
	input,
	button {
		margin: 0;
		padding: 0;
	}

	a,
	li {
		list-style: none;
	}

	a {
		text-decoration: none;
		color: black;
	}

	.login-contain {
		width: 100%;
	}

	.login-header {
		padding-top: 0%;
		padding-bottom: 5%;
		padding-left: 37%;
		padding-right: 5%;
	}

	.login-header img {
		color: #ffffff;
		width: 23%;
		height: 13%;
		z-index: 10;
	}

	.login-logo {
		padding: 5%;
	}

	.login-logo img {
		width: 55px;
		height: 55px;
		border-radius: 50%;
	}

	.login-logo p {
		color: #ffffff;
		font-size: 14px;
		text-align: center;
		letter-spacing: 2px;
		margin-top: 2%;
	}

	.form-group {
		margin-top: 10%;
		margin-left: 0%;
		padding-top: 5%;
		padding-bottom: 5%;
		padding-left: 5%;
		padding-right: 5%;
	}

	.form-group .form-item {
		margin-top: 5%;
		padding: 0 40px;
		border-radius: 20px;
		background-color: #FFFFFF;
	}

	.form-group .form-item input {
		outline: none;
		border: 0;
		border-bottom: 1px solid #f0f0f0;
		border-top: 1px solid #ffffff;
		border-left: 1px solid #ffffff;
		border-right: 1px solid #ffffff;
		background-color: transparent;
		color: #000000;
		height: 40px;
		font-size: 18px;
		width: 85%;
		margin-left: 0%;
		padding-left: 12%;
		padding-bottom: 2%;
	}

	.form-group .form-item input::-webkit-input-placeholder {
		/* WebKit browsers */
		color: #ffffff;
		font-size: 16px;
	}

	.form-group .form-item input:-moz-placeholder {
		/* Mozilla Firefox 4 to 18 */
		color: #ffffff;
		font-size: 16px;
	}

	.form-group .form-item input::-moz-placeholder {
		/* Mozilla Firefox 19+ */
		color: #ffffff;
		font-size: 16px;
	}

	.form-group .form-item input:-ms-input-placeholder {
		/* Internet Explorer 10+ */
		color: #ffffff;
		font-size: 16px;
	}

	.form-group .form-item label img {
		width: 20px;
		height: 25px;
		position: absolute;
		margin-top: 8px;
	}

	.form-group .form-item button {
		outline: none;
		background: transparent;
		border: 1px #00cc99 dashed;
		color: #ffffff;
		height: 30px;
		border-radius: 5px;
		float: right;
		padding: 1%;
	}

	.button-group {
		padding: 5%;
	}

	.button-group button {
		outline: none;
		border: 0;
		width: 90%;
		height: 35px;
		margin-top: 4%;
		border-radius: 20px;
		margin-left: 4%;
		color: #ffffff;
		font-size: 18px;
	}

	.button-group .login-btn {
		background-color: #2394FB;
		color: #FFFFFF;
		line-height: 35px;
	}

	.order-login {
		padding: 5%;
	}

	.order-login-line {
		display: block;
		position: relative;
		text-align: center;
		font-size: 14px;
		color: #bababa;
	}

	.order-login-line:before,
	.order-login-line:after {
		content: '';
		position: absolute;
		top: 50%;
		background: #bababa;
		width: 20%;
		height: 1px;
	}

	.order-login-line:before {
		left: 10%;
		background: #bababa;
		width: 20%;
		height: 1px;
	}

	.order-login-line:after {
		right: 10%;
	}

	.order-login-box {
		display: flex;
		width: 100%;
		justify-content: center;
		margin-top: 20px;
	}

	.order-login-box a {
		width: 45px;
		height: 45px;
		margin: 0px auto;
		text-align: center;
		display: inline-block;
	}

	.order-login-box div {
		flex: 1;
		text-align: center;
	}

	.order-login-box div p {
		text-align: center;
		font-size: 14px;
		color: #ffffff;
	}
</style>
<style  lang="scss">
	/* 分类 */
	.cate-section {
		display: flex;
		flex: 1;
		justify-content: space-around;
		align-items: center;
		flex-wrap: wrap;
		padding: 30upx 22upx;
		background: #fff;

	.cate-item {
		display: flex;
		flex-direction: column;
		align-items: center;
		font-size: 24upx + 2upx;
		color: #303133;
	}

	/* 原图标颜色太深,不想改图了,所以加了透明度 */
	image {
		width: 88upx;
		height: 88upx;
		margin-bottom: 14upx;
		border-radius: 50%;
		opacity: .7;
		box-shadow: 4upx 4upx 20upx rgba(3, 0, 250, 0.3);
	}
	}
	.confirm-btn{
		width: 630upx;
		height: 76upx;
		line-height: 76upx;
		border-radius: 50px;
		margin-top: 70upx;
		background:#2394fb;
		color: #fff;
		font-size:  32upx;
		&:after{
			border-radius: 100px;
		}
	}
</style>
