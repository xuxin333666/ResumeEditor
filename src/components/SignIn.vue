<template>
    <div class="signIn content wrapper">
        <form @submit.prevent action="" method="post" >
            <div class="username bt-input">
                <svg class="icon" aria-hidden="true">
                    <use :xlink:href="`#icon-user`"></use>
                </svg>
                <input @blur="formMatch(0,signInData.username)" :class="{error:!rule[0].status}" v-model="signInData.username" type="text" name="username" autocomplete="off" placeholder="用户名为6-14位数字、字母、下划线">
                <span v-if="signInData.username" @click="signInData.username = ''" class="empty">X</span>
            </div>
            <div class="password bt-input">
                <svg class="icon" aria-hidden="true">
                    <use :xlink:href="`#icon-password`"></use>
                </svg>
                <input @blur="formMatch(1,signInData.password)" :class="{error:!rule[1].status}" v-model="signInData.password" type="password" name="password" autocomplete="off" placeholder="密码为6-14位数字、字母、下划线">
                <span v-if="signInData.password" @click="signInData.password = ''" class="empty">X</span>
            </div>
            <div class="password2 bt-input">
                <svg class="icon" aria-hidden="true">
                    <use :xlink:href="`#icon-password`"></use>
                </svg>
                <input @blur="passwordMatch()" :class="{error:!rule[2].status}" v-model="signInData.password2" type="password" name="password2" autocomplete="off" placeholder="请再次输入密码">
                <span v-if="signInData.password2" @click="signInData.password2 = ''" class="empty">X</span>
            </div>
            <div class="phone bt-input">
                <svg class="icon" aria-hidden="true">
                    <use :xlink:href="`#icon-Phone`"></use>
                </svg>
                <input  @blur="formMatch(3,signInData.phone)" :class="{error:!rule[3].status}" v-model="signInData.phone" type="text" name="phone" autocomplete="off" placeholder="留个电话，方便联系~(可选项)">
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
    data(){
        return {
            rule:[
                {
                    reg: /^\w{6,14}$/,
                    message: '用户名请输入6-14位数字、字母、下划线',
                    status: true
                },
                {
                    reg: /^\w{6,14}$/,
                    message: '密码请输入6-14位数字、字母、下划线',
                    status: true
                },
                {
                    message: '密码应与第一次保持一致',
                    status: true
                },
                {
                    reg: /^1\d{10}$/,
                    message: '请输入合法的手机号',
                    status: true
                }
            ]
        }       
    },
    methods: {
        signIn(){
            let isRight = true;
            for(var i = 0;i < 3;i++){
                if(!this.rule[i].status){
                    this.messages('注册失败，关键信息还没有输入完全','warning');
                    isRight = false;                  
                }               
            }              
            if(isRight){
                this.$emit('signIn')
            }
        },
        turnToLogin(){
            this.$emit('turnToLogin');
        },
        messages(str,str2){
            this.$message({
                message: str,
                type: str2,
                center: true
            });
        },
        formMatch(n,str){
            let arr = this.rule[n];
            if(!arr.reg.test(str)){
                this.messages(arr.message,'warning');
                arr.status = false;
            }else{
                arr.status = true;
            }
        },
        passwordMatch(){
            let arr = this.rule[2];
            if(this.signInData.password !== this.signInData.password2){
                this.messages(arr.message,'warning'); 
                arr.status = false;     
            }else{
                arr.status = true;
            }
        }
    }
}
</script>
<style lang=scss>
    .signIn svg.icon {
        fill: #e81414;
        opacity: 0.4;
    }
    .signIn>form>.bt-input.phone>svg.icon {
        fill: #645e5e;
    }
    .signIn>form>.bt-input>input.error {
        color: red;
    }
</style>


