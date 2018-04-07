<template>
    <div class="dialog">
        <h1  class="header wrapper">ResumeEditor</h1>
        <div class="logo"></div>
        <Login v-if="loginOrSign === 'login'" v-on:turnToSign="loginOrSign = 'sign'" :loginData="loginData" v-on:login="login" />
        <SignIn v-if="loginOrSign === 'sign'" v-on:turnToLogin="loginOrSign = 'login'" :signInData="signInData" v-on:signIn="signIn" />
        <!-- <footer class="wrapper">
            <p class="statement">Love.ly Personal Blog .PSD Template 
                <a href="https://baidu.com" class="copyright footerlink">Copyright ©2018 Matt Gentile</a><br>
                <a href="" class="ad footerlink">Love.ly Home</a><span> |</span>
                <a href="" class="ad footerlink">Bolg</a><span> |</span>
                <a href="" class="ad footerlink">Work</a><span> |</span>
                <a href="" class="ad footerlink">Terms of Use</a><span> |</span>
                <a href="" class="ad footerlink">Contact Me</a>
            </p>
        </footer> -->
    </div>
</template>
<script>
import Login from './Login'
import SignIn from './SignIn'
import AV from 'leancloud-storage'
var APP_ID = '0N7uC2niE1R8CL85PDvLsO20-gzGzoHsz';
var APP_KEY = 'RjJrlzDHVWh4JgWcGhxcb9vr';
AV.init({
  appId: APP_ID,
  appKey: APP_KEY
});
export default {  
    components: {
        Login,
        SignIn
    },
    data(){
        return {
            loginOrSign: 'login',
            loginData: {
                isRememberUser: false,
                username: '',
                password: ''
            },
            signInData: {
                username: '',
                password: ''
            }
        }
    },
    created(){
        this.loginData.username = window.localStorage.getItem('myUsername') || '';
        this.loginData.isRememberUser = window.localStorage.getItem('rememberStatus') || false;
    },
    methods: {
        login(){
            AV.User.logIn(this.loginData.username, this.loginData.password).then((loginedUser) => {
                console.log(loginedUser); 
                this.rememberUser();       
                this.$emit('login');
            }, function (error) {
                console.log(error)
                alert(error)
            });
        },
        signIn(){
            console.log(1)
            let user = new AV.User();
            user.setUsername(this.signInData.username);
            user.setPassword(this.signInData.password);
            user.signUp().then((loginedUser) => {
                console.log(loginedUser);
                alert('注册成功!')
                this.loginOrSign = 'login';
                this.loginData.username = this.signInData.username;
                this.loginData.password = this.signInData.password;
            }, function (error) {
                console.log(error)
                alert(error)
            });
        },
        rememberUser(){
            if(this.loginData.isRememberUser){
                window.localStorage.setItem('myUsername',this.loginData.username);
                window.localStorage.setItem('rememberStatus',this.loginData.isRememberUser);
            return;
            }
            window.localStorage.removeItem('myUsername');
            window.localStorage.removeItem('rememberStatus');
        }
    }
}
</script>
<style lang=scss>
.dialog {
    height: 100%;
    padding: .1px;
    background: #d8d0cd;
    .wrapper {
        width: 400px;
        margin: 0 auto;
        margin-top: 50px;
        text-align: center;
    }
    /* header css */
    .header {
        color: #635b58;
    }
    /* content css */
    >.content {
        padding-top: 10px;
        padding-bottom: 40px;
        background: #e5e2dd;
        border-radius: 6px;
        box-shadow:0 0px 10px rgba(0, 0, 0, 0.15),0 0px 12px rgba(0, 0, 0, 0.2);
        overflow: hidden;
    }
    form>div {
        margin-left: 35px;
        margin-right: 35px;
    }
    svg.icon {
        width: 20px;
        height: 20px;
        fill: #645e5e;
        opacity: 0.6;
    }
    .bt-input {
        margin-top: 30px;
        padding-left: 10px;
        font-size: 14px;
        background: #e3dbd8;
        box-shadow: inset 0 -2px 3px rgba(0, 0, 0, .3), inset 0 2px 3px rgba(0, 0, 0, 0.3);
        width: 320px;
        height: 50px;
        text-align: left;
        border-radius: 8px;
        display: flex;
        align-items: center;
    }
    .bt-input>input {
        margin-left: 10px;
        width: 83%;
        height: 80%;
        border: none;
        outline: none;
        background: #e3dbd8;
        color: #645e5e;
        font-weight: bold;
    }
    .bt-input>.empty {
        color: #645e5e;
        cursor: pointer;
    }
    .orther {
        margin-top: 30px;
        text-align: left;
        line-height: 50px;
    }
    .orther>.rememberme {
        font-size: 18px;
        font-weight: bold;
        vertical-align: middle;
        color: #635b58;
    }
    #rememberme {
        -webkit-appearance: none;
        width: 40px;
        height: 40px;
        background: url('http://p6o0v7chj.bkt.clouddn.com/%E6%9C%AA%E7%82%B9%E9%80%89-%E5%9C%86%E5%BD%A2%E9%80%89%E6%A1%86.png') no-repeat;
        background-size: contain;
        outline: none;
    }
    #rememberme:checked {
        background: url('http://p6o0v7chj.bkt.clouddn.com/%E7%82%B9%E9%80%89-%E5%9C%86%E5%BD%A2%E9%80%89%E6%A1%86.png') no-repeat;
        background-size: contain;
    }
    .orther>.turnTo {
        font-size: 14px;
        color: #9a928f;
        font-weight: bold;
        cursor: pointer;
    }
    .submit {
        margin-top: 20px;
        width: 330px;
        padding: 10px 0;
        display: inline-block;
        vertical-align: middle;
        cursor: pointer;
        outline: none;
        border: none;
        box-shadow:0 0px 10px rgba(0, 0, 0, 0.15),0 0px 12px rgba(0, 0, 0, 0.2);
        border-radius: 14px;
        font-size: 20px;
        color: white;
        background: linear-gradient(#98ad71, #657843);
    }
    .submit:hover {
        opacity: 0.85;
    }
    footer.wrapper {
        width: 460px;
        margin-left: auto;
        margin-right: auto;
        font-size: 14px;
        font-weight: bold;
        color: #635b58;
    }
    .footerlink {
        color: #9a928f;
        text-decoration: underline;
    }
}

</style>
