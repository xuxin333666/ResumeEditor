<template>
    <div class="dialog">
        <h1  class="header wrapper">VueResume Editor</h1>
        <Login v-if="loginOrSign.key === 'login'" v-on:turnToSign="loginOrSign.key = 'sign'" :loginData="loginData" v-on:login="login"  />
        <SignIn v-if="loginOrSign.key === 'sign'" v-on:turnToLogin="loginOrSign.key = 'login'" :signInData="signInData" v-on:signIn="signIn"  />
    </div>
</template>
<script>
import Login from './Login'
import SignIn from './SignIn'
export default {  
    props:['loginData','signInData','loginOrSign'],
    components: {
        Login,
        SignIn
    },
    data(){
        return {
        }
    },
    methods: {
        login(){
            this.$emit('login')
        },
        signIn(){
            this.$emit('signIn')
        },
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
        background: #e3dbd8;
        font-size: 14px;
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
    }
    .bt-input>input::-webkit-input-placeholder {
        font-size: 13px;
        opacity: 0.4;
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
