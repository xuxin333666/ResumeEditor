<template>
  <div>
    <h3 class="logo">VueResumer</h3>
    <div class="headButton">
      <el-button @click="logOut()" type="success" round>登出</el-button>
      <el-button @click="preview()" type="primary" round>预览</el-button>
      <el-button @click="saveData()" type="success" round>保存</el-button>
      <el-button @click="buildNew()" type="primary" round>新建</el-button>
    </div>

  </div>
</template>
<script>
export default {
  methods:{
    logOut(){
      this.$emit('logOut')
    },
    preview(){
      this.$emit('preview');
    },
    saveData(){
      this.$emit('saveData');
    },
    buildNew(){
      this.$emit('buildNew');
    }
  }
}
</script>

<style lang=scss>
.topbar {
  padding: 16px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  >.headButton>button {
    padding: 8px 12px;
  }
}
</style>

