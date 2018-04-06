<template>
  <div :class="{hidden:hiddenStatus}" id="app">
    <Topbar v-on:preview="preview" class="topbar"/>
    <main>
      <Editor :resume="resume" class="editor"/>
      <Preview :resume="resume" class="preview"/>
      <el-button type="primary" @click="hiddenStatus = false" class="quit" plain>退出预览</el-button>
    </main>
  </div>
</template>

<script>
import Topbar from './components/Topbar'
import Editor from './components/Editor'
import Preview from './components/Preview'
export default {
  name: 'App',
  components: {
    Topbar,
    Editor,
    Preview
  },
  data(){
    return {
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
    preview(){
      this.hiddenStatus = true;
    }
  }
}
</script>

<style lang=scss>
body,html,#app {
  height: 100%;
}
body {
  #app.hidden {
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
  .topbar {
    position: relative;
    z-index: 1;
    width: 100%;
    height: 7%;
    box-shadow: 0 5px 6px rgba(0, 0, 0, 0.2),0 2px 8px rgba(0, 0, 0, 0.2)
  }
  main {
    display: flex;
    height: 93%;
    padding: 16px;
    background: #e2e2e2;
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
