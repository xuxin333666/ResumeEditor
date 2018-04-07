<template>
  <div :class="{hidden:hiddenStatus,login:loginStatus}" id="app">
    <Dialog v-on:login="loginStatus = true" class="dialog" :class="{hidden:loginStatus}"/>
    <Topbar v-on:quitLogin="loginStatus = false" v-on:preview="hiddenStatus = true" v-on:saveData="saveData" v-on:buildNew="buildNew" class="topbar"/>
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
  },
  data(){
    return {
      loginStatus: false,
      hiddenStatus: false,
      resume: null
    }
  },
  methods: {
    saveData(){
      window.localStorage.setItem('myResume',JSON.stringify(this.resume));
    },
    buildNew(){
      var resume = {
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
      window.localStorage.setItem('myResume',JSON.stringify(resume));
      location.reload();
    }
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
