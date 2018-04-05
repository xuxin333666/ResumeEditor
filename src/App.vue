<template>
  <div id="app">
    <Topbar class="topbar"/>
    <main>
      <Editor class="editor"/>
      <Preview class="preview"/>
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
  }
}
</script>

<style lang=scss>
body,html,#app {
  height: 100%;
}
body {
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
    }
  }
}


</style>
