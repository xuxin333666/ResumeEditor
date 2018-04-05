<template>
  <div class="topbar">
    <h3 class="logo">VueResumer</h3>
    <div class="headButton">
      <el-button type="primary" round>注册</el-button>
      <el-button type="success" round>登录</el-button>
    </div>

  </div>
</template>
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

