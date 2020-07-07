<template>
    <div class="login">
        <div class="login-wrapper">
            <div class="logo-wrapper">
                <div class="logo-center">
                    <img src="../../static/img/logo@2x.png" style="margin: 60px auto;">
                </div>
            </div>
            <div class="login-content">
                <div class="login-center clearfix">
                    <div class="login-center-input">
                        <div class="login-center-img"><img src="../../static/img/icon_iphone@2x.png"></div>
                        <input type="text" v-model="username" placeholder="请输入您的手机号码">
                    </div>
                </div>

                <div class="login-center clearfix">
                    <div class="login-center-input">
                        <div class="login-center-img"><img src="../../static/img/icon_password@2x.png"></div>
                        <input type="password" v-model="password"  placeholder="请输入您的密码">
                    </div>
                </div>
            </div>
            <div class="button-group">
                <button class="login-btn" id="doLogin" @tap="bindLogin">登录</button>
            </div>
            <div class="order-login">
                <p class="order-login-line">第三方账号登录</p>
                <div class="order-login-box">
                
                        <a href="#">
                            <img src="../../static/img/icon_weixin@2x.png" alt="" id= "activity"  @tap="bindRecuperationOne" >
                        </a>
                    
                  
                        <a href="#">
                            <img src="../../static/img/icon_qq@2x.png" alt="" style="width: 45px;height: 45px;">
                        </a>
                   
                   
                        <a href="#">
                            <img src="../../static/img/icon_weibo@2x.png" alt="" style="width: 45px;height: 45px;">
                        </a>
                  
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
	    data () {
	       return {
			 isActive: false,
	         username: '',
	         password: '',
	       }
	   },
        methods: {
			bindRecuperationOne(){
				if (this.isActive) {
					document.getElementById("activity").style = "transform:scale(1)";
					this.isActive = false;
				} else {
					document.getElementById("activity").style = "transform:scale(1.5)";
					this.isActive = true;
				}
			},
            bindLogin() {
				uni.request({
				    url: 'http://localhost:2009/app/account/login', //仅为示例，并非真实接口地址。
					method:'POST',
				    data: {
				        username: this.username,
						password:this.password,
						ip:'',
				    },
					header: {
					        'content-type': 'application/x-www-form-urlencoded' //自定义请求头信息
					},
				    success: (res) => {
				     console.log(res)
					if(res.data.code==200){
						uni.reLaunch({
						    url: '../main/main',
						});					  
					}else{
						uni.reLaunch({
						    url: '../user/user',
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

<style>
    *{margin:0;padding:0}
    .logo-wrapper {
        background-image: url(../../static/img/bg@2x.png); background-size:cover ;
        width:100%;
        height:225px;
        margin-top: -71px;
        margin-bottom: 10px;
		opacity: 1;
    }
    .login-content{
        padding-top:5px;
    }
    .logo-center img {
        padding-left: 135px;
        width: 100px;
        height: 100px;
        display: inline-block;
    }

    .login {
        z-index: 2;
        position: absolute;
        width: 374px;
        height: 575px;
        top: 50%;
        left: 50%;
        margin-top: -261px;
        margin-left: -188px;
    }

    .login-top {
        font-size: 24px;
        margin-top: 100px;
        padding-left: 40px;
        box-sizing: border-box;
        color: #333333;
        margin-bottom: 50px;
    }

    .login-center {
        width: 100%;
        box-sizing: border-box;
        padding: 12px 40px;
        margin-bottom: 30px;
    }

    .login-center-img {
        width: 20px;
        height: 20px;
        float: left;
        margin-top: 5px;
        padding-top:5px;
        display:inline-block;
    }

    .login-center-img>img {
        position: absolute;
        z-index: 100;
        width: 20px;
        height: 25px;
        margin-bottom:5px;
        padding-bottom: 5px;
        padding-top:17px;
        display:inline-block;
    }

    .login-center-input {
        float: left;
        width: 230px;
        margin-left: 15px;
        margin: 15px;
        height: 30px;
        position: relative;
    }

    .login-center-input input {
        font-size: 17px;
        z-index: 2;
        padding-left: 35px;
        padding-bottom:15px;
        width: 110%;
        height: 35px;
        border: 0;
        border-bottom: 1px solid #f0f0f0;
        border-top: 1px solid #ffffff;
        border-left: 1px solid #ffffff;
        border-right: 1px solid #ffffff;
        box-sizing: border-box;
        outline: none;
        position: relative;
    }
    .login-button {
        cursor: pointer;
        width: 250px;
        text-align: center;
        height: 40px;
        line-height: 40px;
        background-color: dodgerblue;
        border-radius: 5px;
        margin: 0 auto;
        margin-top: 50px;
        color: white;
    }

    .button-group {
        padding: 5%;
        padding-top:60px;
    }

    .button-group button {
        outline: none;
        border: 0;
        width: 90%;
        height: 42px;
        margin-top: 4%;
        border-radius: 20px;
        margin-left: 4%;
        color: #ffffff;
        font-size: 18px;
    }

    .button-group .login-btn {
        background-color: #2394fb;
    }

    .order-login {
        padding: 10%;
        padding-bottom: 10px;
    }

    .order-login-line {
        display: block;
        position: relative;
        padding-top:10px;
        padding-bottom: 13px;
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
		height:45px;
		margin: 0px auto;
        text-align: center;
		display: inline-block;
    }

    .order-login-box div p {
        text-align: center;
        font-size: 14px;
        color: #ffffff;
    }

</style>
