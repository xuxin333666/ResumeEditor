<template>
    <div class="login content wrapper">
        <form @submit.prevent action="" method="post" >
            <div class="username bt-input">
                <svg class="icon" aria-hidden="true">
                    <use :xlink:href="`#icon-user`"></use>
                </svg>
                <input v-model="loginData.username" type="text" id="username" class="username" name="username" autocomplete="off" placeholder="亲，这里输入用户名哦~">
                <span v-if="loginData.username" @click="loginData.username = ''" class="empty">X</span>
            </div>
            <div class="password bt-input">
                <svg class="icon" aria-hidden="true">
                    <use :xlink:href="`#icon-password`"></use>
                </svg>
                <input v-model="loginData.password" type="password" id="password" class="password" name="password" autocomplete="off" placeholder="亲，确保周围环境再输入密码哦~">
                <span v-if="loginData.password" @click="loginData.password = ''" class="empty">X</span>
            </div>
            <div class="orther">
                <input @click="rememberTips" v-model="loginData.isRememberUser" type="checkbox" id="rememberme" class="rememberme" name="rememberme" value="rememberme">
                <label for="rememberme" class="rememberme">Remember Me</label><br>
                <span @click="turnToSign" class="turnTo">还没有用户名？点击这里注册一个吧</span>
            </div>
            <input type="submit" value="登录" @click="login" class="submit">
        </form>
    </div>
</template>
<script>
export default {
    props:['loginData'],
    data(){
        return{
            rememberTip: false 
        }
    },
    methods: {
        login(){
            this.$emit('login');
        },
        turnToSign(){
            this.$emit('turnToSign');
        },
        rememberTips(){
            if(this.rememberTip){
                return;
            }
            this.rememberTip = true;
            this.$notify.info({
                title: '消息',
                message: '设置在登录后生效~'
            });
        }
    }
}
</script>

