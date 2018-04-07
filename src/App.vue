<template>
  <div :class="{hidden:hiddenStatus,login:currentUser !==null}" id="app">
    <Dialog  class="dialog" :class="{hidden:currentUser !==null}" v-on:login="login"  v-on:signIn="signIn"  :loginData="loginData" :signInData="signInData" :loginOrSign="loginOrSign"/>
    <Topbar v-on:logOut="logOut" v-on:preview="hiddenStatus = true" v-on:saveData="saveData" v-on:buildNew="buildNew" class="topbar" :currentUser="currentUser"/>
    <main>
      <Editor :resume="resume" class="editor"/>
      <Preview :resume="resume" class="preview"/>
      <el-button type="primary" @click="hiddenStatus = false" class="quit" plain>退出预览</el-button>
    </main>
  </div>
</template>
<script>
import Dialog from './components/Dialog'
import Topbar from './components/Topbar'
import Editor from './components/Editor'
import Preview from './components/Preview'
import AV from 'leancloud-storage'
var APP_ID = '0N7uC2niE1R8CL85PDvLsO20-gzGzoHsz';
var APP_KEY = 'RjJrlzDHVWh4JgWcGhxcb9vr';
AV.init({
  appId: APP_ID,
  appKey: APP_KEY
});
export default {
  name: 'App',
  components: {
    Topbar,
    Editor,
    Preview,
    Dialog
  },
  created(){
      var myResume = {
        personal: {
          '姓名': '',
          '年龄': '',
          '城市': ''
        },
        workMain: [{
          '公司': '',
          '工作经历': ''
        }],
        stady: [{
          '起始日期': '',
          '学校': '',
          '学位/专业': '',
          '在校经历': '',
        }],
        project: [{
          '项目名称': '',
          "项目内容": '',
          "学到了？": ''
        }],
        prize: [{
          '获奖时间': '',
          '奖项名称': ''
        }],
        contact: {
          "电话": '',
          "微信": '',
          "电子邮箱": '',
          "GitHub": ''
        }
      };
      this.resume = JSON.parse(window.localStorage.getItem('myResume')) || myResume;
      this.loginData.username = window.localStorage.getItem('myUsername') || '';
      this.loginData.isRememberUser = window.localStorage.getItem('rememberStatus') || false;
      this.getCurrentUser();
  },
  data(){
    return {
      loginOrSign: {
        key: 'login'
      },
      loginData: {
          isRememberUser: false,
          username: '',
          password: ''
      },
      signInData: {
          username: '',
          password: '',
          password2: '',
          phone: '',
      },
      currentUser: null,
      hiddenStatus: false,
      resume: null,
    }
  },
  methods: {
    logOut(){
      AV.User.logOut();
      window.location.reload();
    },
    login(){
        AV.User.logIn(this.loginData.username, this.loginData.password).then((loginedUser) => {
            this.getCurrentUser();
            this.rememberUser(); 
            this.message('登录成功！','success')    
        },(error) => {
            this.message('用户名或密码错误','warning')
        });
    },
    signIn(){
        let user = new AV.User();
        user.setUsername(this.signInData.username);
        user.setPassword(this.signInData.password);
        user.signUp().then((loginedUser) => {
            this.message('恭喜您，账号注册成功','success')
            this.loginOrSign.key = 'login';
            this.loginData.username = this.signInData.username;
            this.loginData.password = this.signInData.password;
        }, (error) => {
            this.message('该账号已经被注册了','warning');
                            
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
    },
    getCurrentUser(){
        let current = AV.User.current()
        if (current) {
            let {id,createdAt,attributes:{username}} = current;
            this.currentUser = {id,createdAt,username};
        }
    },
    saveData(){
      window.localStorage.setItem('myResume',JSON.stringify(this.resume));
      // let dataString = JSON.stringify(this.resume);
      // var AVResume = AV.Object.extend('AllResume');
      // var avResume = new AVResume();
      // avResume.set('content', dataString);
      // avResume.save().then(function (todo) {
      //   alert('保存成功');
      // }, function (error) {
      //   alert('保存失败');
      // });
    },
    buildNew(){
      window.localStorage.removeItem('myResume');
      window.location.reload();
    },
    message(str,str2){
      this.$message({
          message: str,
          type: str2,
          center: true
      });
    },
  }
}
</script>
<style lang=scss>
body,html,#app {
  height: 100%;
}
body {
  #app.login.hidden {
    >.topbar,>main>.editor {
      display: none;
    }
    >main {
      height: 100%;
      >.preview {
        max-width: 850px;
        min-width: 700px;
        margin-left: auto;
        margin-right: auto;
      }
      >.quit {
        display: block;
      }
    }
  }
  #app.login {
    >.topbar,>main {
      display: flex;
    }
  }
  .dialog.hidden {
    display: none;
  }
  .topbar {
    display: none;
    position: relative;
    z-index: 1;
    width: 100%;
    height: 7%;
    box-shadow: 0 5px 6px rgba(0, 0, 0, 0.2),0 2px 8px rgba(0, 0, 0, 0.2)
  }
  main {
    display: none;
    height: 93%;
    padding: 16px;
    background: #e3dbd8;
    >.editor,.preview {
      display: flex;
      background: white;
      position: relative;
      z-index: 1;
      box-shadow: 0 0 6px rgba(0, 0, 0, 0.2),0 0 8px rgba(0, 0, 0, 0.2);
    }
    >.editor {
      width: 550px;
      margin-right: 16px;
    }
    >.preview {
      flex: 1;
      overflow: auto;
    }
    >.quit {
      display: none;
      position: fixed;
      bottom: 50px;
      right: 20%;
      z-index: 1;
    }
  }
}


</style>
