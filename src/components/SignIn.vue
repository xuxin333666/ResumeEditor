<template>
    <div class="signIn content wrapper">
        <form @submit.prevent action="" method="post" >
            <div class="username bt-input">
                <svg class="icon" aria-hidden="true">
                    <use :xlink:href="`#icon-user`"></use>
                </svg>
                <input v-model="signInData.username" type="text" id="username" class="username" name="username" placeholder="亲，这里输入用户名哦~">
                <span v-if="signInData.username" @click="signInData.username = ''" class="empty">X</span>
            </div>
            <div class="password bt-input">
                <svg class="icon" aria-hidden="true">
                    <use :xlink:href="`#icon-password`"></use>
                </svg>
                <input v-model="signInData.password" type="password" id="password" class="password" name="password" placeholder="亲，确保周围环境再输入密码哦~">
                <span v-if="signInData.password" @click="signInData.password = ''" class="empty">X</span>
            </div>
            <div class="orther">
                <span @click="turnToLogin" class="turnTo">已经注册了？点击这里立刻登录把</span>
            </div>
            <input type="submit" value="注册" @click="signIn" class="submit">
        </form>
    </div>
</template>
<script>
export default {
    props:['signInData'],
    methods: {
        signIn(){
            this.$emit('signIn')
        },
        turnToLogin(){
            this.$emit('turnToLogin');
        }
    }
}
</script>

