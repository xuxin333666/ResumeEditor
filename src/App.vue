<template>
  <div id="app">
    <Topbar class="Topbar"/>
    <main>
      <Editor class="Editor"/>
      <Preview class="Preview"/>
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

<style>

</style>
