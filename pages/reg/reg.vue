<template>
	<view class="content">
		<view class="input-group">
			<view class="input-row border">
				<text class="title">用户：</text>
				<m-input type="text" focus clearable v-model="username" placeholder="请输入用户"></m-input>
			</view>
			<view class="input-row border">
				<text class="title">密码：</text>
				<m-input type="password" displayable v-model="password" placeholder="请输入密码"></m-input>
			</view>
			<view class="input-row">
				<text class="title">手机：</text>
				<m-input type="text" clearable v-model="mobile" placeholder="请输入手机号"></m-input>
			</view>
		</view>
		<view class="btn-row">
			<button type="primary" class="primary" @tap="register">注册</button>
		</view>
	</view>
</template>

<script>
	// import service from '../../service.js';
	import mInput from '../../components/m-input.vue';

	export default {
		components: {
			mInput
		},
		data() {
			return {
                username: '',
				password: '',
                mobile: ''
			}
		},
		methods: {
			register() {
				/**
				 * 客户端对账号信息进行一些必要的校验。
				 * 实际开发中，根据业务需要进行处理，这里仅做示例。
				 */
				if (this.username.length < 4) {
					uni.showToast({
						icon: 'none',
						title: '账号最短为 5 个字符'
					});
					return;
				}
				if (this.password.length < 6) {
					uni.showToast({
						icon: 'none',
						title: '密码最短为 6 个字符'
					});
					return;
				}
				if (this.mobile.length < 11 ) {
                    uni.showToast({
                        icon: 'none',
                        title: '手机最短为 11 个字符'
                    });
                    return;
				}
                uni.request({
                    url: 'http://localhost:2009/app/account/username-register',
					method: 'POST',
                    data:{
                        username: this.username,
                        password: this.password,
                        mobile: this.mobile
					},
                    header: {
                        'content-type': 'application/x-www-form-urlencoded' //自定义请求头信息
                    },
                    success: (res) => {

                        uni.showToast({
                        	title: '注册成功'
                        });
						console.log(res+"test")
						if(res.data.code == 200){
							
							// uni.request({
							//     url: 'http://localhost:2009/app/medical/patientinfo-init',
							// 	method: 'POST',
							//     data:{
							//         name: this.username,
							//         tel: this.mobile
							// 	},
							//     header: {
							//         'content-type': 'application/json' //自定义请求头信息
							//     },
							//     success: (res) => {
							
							//       console.log("初始化成功")
							
							//     }
							// });
					
                            uni.reLaunch({
                                url: '../login/login',
								
                            });
						}

                    }
                });
				
			}
		}
	}
</script>

<style>

</style>
