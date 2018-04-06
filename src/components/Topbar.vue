<template>
  <div>
    <h3 class="logo">VueResumer</h3>
    <div class="headButton">
      <el-button type="primary" round>注册</el-button>
      <el-button type="success" round>登录</el-button>
      <el-button @click="preview()" type="primary" round>预览</el-button>
    </div>

  </div>
</template>
<script>
export default {
  methods:{
    preview(){
      this.$emit('preview');
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

