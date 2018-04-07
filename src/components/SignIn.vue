<template>
    <div class="signIn content wrapper">
        <form @submit.prevent action="" method="post" >
            <div class="username bt-input">
                <svg class="icon" aria-hidden="true">
                    <use :xlink:href="`#icon-user`"></use>
                </svg>
                <input v-model="signInData.username" type="text" id="username" class="username" name="username" placeholder="用户名为6-20位数字、字母、下划线">
                <span v-if="signInData.username" @click="signInData.username = ''" class="empty">X</span>
            </div>
            <div class="password bt-input">
                <svg class="icon" aria-hidden="true">
                    <use :xlink:href="`#icon-password`"></use>
                </svg>
                <input v-model="signInData.password" type="password" id="password" class="password" name="password" placeholder="密码为6-20位数字、字母、下划线">
                <span v-if="signInData.password" @click="signInData.password = ''" class="empty">X</span>
            </div>
            <div class="password2 bt-input">
                <svg class="icon" aria-hidden="true">
                    <use :xlink:href="`#icon-password`"></use>
                </svg>
                <input v-model="signInData.password2" type="password" id="password2" class="password2" name="password2" placeholder="请再次输入密码">
                <span v-if="signInData.password2" @click="signInData.password2 = ''" class="empty">X</span>
            </div>
            <div class="phone bt-input">
                <svg class="icon" aria-hidden="true">
                    <use :xlink:href="`#icon-Phone`"></use>
                </svg>
                <input v-model="signInData.phone" type="text" id="phone" class="phone" name="phone" placeholder="留个电话，方便联系~(可选项)">
                <span v-if="signInData.phone" @click="signInData.phone = ''" class="empty">X</span>
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
<style lang=scss>
    .signIn svg.icon {
        fill: red;
    }
    .signIn>form>.bt-input.phone>svg.icon {
        fill: #645e5e;
    }
</style>


