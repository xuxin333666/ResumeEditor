<template>
  <div :class="{hidden:hiddenStatus,login:currentUser !==null}" id="app">
    <Dialog  class="dialog" :class="{hidden:currentUser !==null}" v-on:login="login"  v-on:signIn="signIn"  :loginData="loginData" :signInData="signInData" :loginOrSign="loginOrSign"/>
    <div class="topbarCt">
        <Topbar v-on:logOut="logOut" v-on:preview="hiddenStatus = true" v-on:saveData="saveData" v-on:buildNew="buildNew" class="topbar" :currentUser="currentUser"/> 
    </div>
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
      this.loginData.username = window.localStorage.getItem('myUsername') || '';
      this.loginData.isRememberUser = window.localStorage.getItem('rememberStatus') || false;
      this.getCurrentUser();
      this.getOldSave();
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
      resume: {
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
      }
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
            this.getOldSave();
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
    updateData: function(){
      let dataString = JSON.stringify(this.resume) 
      let AVResume = AV.Object.createWithoutData('AllResume', this.resume.id)
      AVResume.set('content', dataString)
      AVResume.save().then(()=>{
          this.message('更新成功','success')
      },(error) => {
          this.message('更新失败','warning');
      })
    },
    saveData(){
      if(this.resume.id){
        this.updateData();
      }else{
        let dataString = JSON.stringify(this.resume);
        var AVResume = AV.Object.extend('AllResume');
        var avResume = new AVResume();
        var acl = new AV.ACL();
        acl.setReadAccess(AV.User.current(),true);
        acl.setWriteAccess(AV.User.current(),true);
        avResume.set('content', dataString);
        avResume.setACL(acl);
        avResume.save().then((todo) => {
          this.resume.id = todo.id;
          this.message('保存成功','success')
        }, function (error) {
          this.message('保存失败','warning');
        });
      }
    },
    getOldSave(){
      if(this.currentUser){
        var query = new AV.Query('AllResume');
        query.find().then((todos) => {
          let id = todos[0].id;
          this.resume = JSON.parse(todos[0].attributes.content);
          this.resume.id = id;
        }, function(error){
            console.error(error);
        })
      }
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
  background: #e3dbd8;
}
body {
  #app.login.hidden {
    >.topbarCt,>main>.editor {
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
    >.topbarCt>.topbar,>main {
      display: flex;
    }
  }
  .dialog.hidden {
    display: none;
  }
  .topbarCt {
    box-shadow: 0 5px 6px rgba(0, 0, 0, 0.2),0 2px 8px rgba(0, 0, 0, 0.2);
    >.topbar {
      max-width: 1440px;
      min-width: 960px;
      margin: 0 auto;
      display: none;
      position: relative;
      z-index: 1;
      width: 100%;
      height: 7%;
    }
  }
  main {
    margin: 0 auto;
    display: none;
    max-width: 1440px;
    min-width: 960px;
    height: 93%;
    padding: 16px;
    >.editor,.preview {
      display: flex;
      background: white;
      position: relative;
      z-index: 1;
      box-shadow: 0 0 6px rgba(0, 0, 0, 0.2),0 0 8px rgba(0, 0, 0, 0.2);
    }
    >.editor {
      max-width: 550px;
      min-width: 480px;
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
