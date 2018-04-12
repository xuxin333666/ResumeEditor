<template>
  <div :class="{hidden:hiddenStatus,login:currentUser !==null}" id="app">
    <Dialog  class="dialog" :class="{hidden:currentUser !==null}" v-on:login="login"  v-on:signIn="signIn"  :loginData="loginData" :signInData="signInData" :loginOrSign="loginOrSign"/>
    <div class="topbarCt">
        <Topbar v-on:logOut="logOut" v-on:preview="hiddenStatus = true" v-on:saveData="saveData" v-on:buildNew="buildNew" class="topbar" :stepStatus="stepStatus" :currentUser="currentUser" :resume="resume"/> 
    </div>
    <main>
      <Editor :class="{turn:!(turn%2)}" :resume="resume" class="editor"/>
      <div class="turn">
        <svg  @click="turn++" class="icon" aria-hidden="true">
          <use xlink:href="#icon-weibiaoti8"></use>
        </svg>
      </div>
      <Preview :class="{turn:!(turn%2)}" :resume="resume" :avatar="avatar" v-on:upLoadPhoto="upLoadPhoto" class="preview"/>
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
      this.getOldSave('AllResume',this.resume,'content');
      this.getOldSave('_File',this.avatar,'url');
  },
  data(){
    return {
      turn: 1,
      stepStatus: {
        isUploadPhoto: false,
        isEditor: false,
        isSaveData: false
      },
      avatar: {
        url: ''
      },
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
          '姓名': '你的名字',
          '自我简述': '一句话介绍自己，让HR知道选择你的理由',
          '年龄': '填写年龄',
          '城市': '填写所在城市'
        },
        workMain: [{
          '工作时间': '填写时间',
          '公司': '填写公司',
          '职位': '填写职位',
          '工作经历': '填写内容'
        }],
        stady: [{
          '起始日期': '填写时间',
          '学校': '填写学校',
          '学位/专业': '填写专业',
          '在校经历': '填写内容',
        }],
        project: [{
          '项目名称': '填写项目',
          "项目内容": '填写内容',
        }],
        prize: [{
          '获奖时间': '填写时间',
          '奖项名称': '填写内容'
        }],
        contact: {
          "电话": '填写电话',
          "微信": '填写微信',
          "电子邮箱": '填写电子邮箱',
          "GitHub": '填写github地址'
        }
      }
    }
  },
  methods: {
    logOut(){
      if(!this.stepStatus.isSaveData){
        this.isNotSave();
      }else{
        AV.User.logOut();
        window.location.reload();
      }
    },
    login(){
        AV.User.logIn(this.loginData.username, this.loginData.password).then((loginedUser) => {
            this.getCurrentUser();
            this.getOldSave('AllResume',this.resume,'content');
            this.getOldSave('_File',this.avatar,'url');
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
    updateData(){
      let dataString = JSON.stringify(this.resume) 
      let AVResume = AV.Object.createWithoutData('AllResume', this.resume.id)
      AVResume.set('content', dataString)
      AVResume.save().then(()=>{
          this.message('更新成功','success')
          this.stepStatus.isSaveData = true;
      },(error) => {
          this.message('更新失败,请重试','warning');
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
        avResume.set('content', dataString);
        this.ACL(avResume);
        avResume.save().then((todo) => {
          this.resume.id = todo.id;
          this.stepStatus.isSaveData = true;
          this.message('保存成功','success')
        }, function (error) {
          this.message('保存失败,请重试','warning');
        });
      }
    },
    getOldSave(className,dataName,type){
      if(this.currentUser){
        var query = new AV.Query(className);
        query.find().then((todos) => {
          if(type === 'content'){
            this.resume.id = todos[0].id;
            var obj = JSON.parse(todos[0].attributes.content);
            this.forinObj(obj,this.resume);
          }else if(type === 'url'){
            this.avatar.id = todos[todos.length-1].id;
            this.avatar.url = todos[todos.length-1].attributes.url
            this.stepStatus.isUploadPhoto = true;
          }
        }, function(error){
            this.message('获取数据失败,请重试','warning');
        })
      }
    },
    buildNew(){
      window.localStorage.removeItem('myResume');
      window.location.reload();
    },
    upLoadPhoto(){
      var fileUploadControl = document.getElementById('photoFileUpload');
      if (fileUploadControl.files.length > 0) {
        var localFile = fileUploadControl.files[0];
        var name = 'avatar.jpg';
        var avfile = new AV.File(name, localFile);
        this.ACL(avfile);
        avfile.save().then((file) => {
          this.avatar.url = file.url();
          this.avatar.id = file.id;
          this.stepStatus.isUploadPhoto = true;
          this.message('上传成功','success');
        },(error) => {
          this.message('获取头像失败,请重试','warning');
        });
      }
    },
    ACL(av){
      var acl = new AV.ACL();
      acl.setReadAccess(AV.User.current(),true);
      acl.setWriteAccess(AV.User.current(),true);
      av.setACL(acl);
    },
    message(str,str2){
      this.$message({
          message: str,
          type: str2,
          center: true
      });
    },
    forinObj(obj,data){
      for (var key in obj){
        if(obj[key] instanceof Array){
          for(var i = 0; i < obj[key].length; i++){
            this.forinObj(obj[key][i],data[key][i])
          }
        }else if((typeof obj[key])=== 'object'){
          this.forinObj(obj[key],data[key])
        }else{
          data[key] = obj[key]
        }
      }
    },
    isNotSave(){
      this.$confirm('还没有保存简历, 是否继续?', '提示', {
        confirmButtonText: '保存',
        cancelButtonText: '不保存',
        type: 'warning'
      }).then(() => {
        this.saveData();
        setTimeout(()=>{
          AV.User.logOut();
          window.location.reload();  
        },1000) 
      }).catch(() => {
        AV.User.logOut();
        window.location.reload();     
      });
    }
  }
}
</script>
<style lang=scss>
body,html,#app {
  height: 100%;
  min-height: 768px;
  background: #748194;
}
body {
  #app.login.hidden {
    >.topbarCt,>main>.editor,>.turn {
      display: none;
    }
    >main {
      height: 100%;
      >.preview {
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
    min-width: 1024px;
    background: white;
    box-shadow: 0 3px 4px rgba(0, 0, 0, 0.2),0 2px 6px rgba(0, 0, 0, 0.2);
    height: 5%;
    >.topbar {
      max-width: 1440px;
      width: 100%;
      height: 100%;
      padding: 0 16px;
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin: 0 auto;
      display: none;
      position: relative;
      z-index: 1;
    }
  }
  main {
    margin: 0 auto;
    display: none;
    max-width: 1440px;
    min-width: 1024px;
    height: 95%;
    padding: 16px;
    >.editor,.preview {
      display: flex;
      background: white;
      position: relative;
      z-index: 1;
      box-shadow: 0 0 6px rgba(0, 0, 0, 0.2),0 0 8px rgba(0, 0, 0, 0.2);
    }
    >.editor {
      flex: 1;  
      order: 1;  
      min-height: 672px;
      background: #d8cdc7;
    }
    >.editor.turn {
      order: 3;
    }
    >.turn {
      display: flex;
      align-items: center;
      order: 2;
      height: 100%;
      >svg.icon{
        cursor: pointer;
      fill: #6ba7fa;
      margin: 7px;
      width: 36px;
      height: 36px;
      }
      >svg.icon:hover {
        fill: #82b6ff;
      }
    }
    >.preview {
      order: 3;
      cursor: default;
      flex-direction: column;
      flex-wrap: wrap;
      flex: 1;
      max-width: 850px;
      max-height: 100%;
      min-width: 480px;
      min-height: 672px;
      overflow: auto;
    }
    >.preview.turn {
      order: 1;
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
