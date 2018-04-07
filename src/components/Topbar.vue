<template>
  <div>
    <h3 class="logo">VueResumer</h3>
    <div class="headButton">
      <el-button @click="preview" type="primary" round>预览</el-button>
      <el-dropdown  @command="handleCommand" class="menu">
        <span class="el-dropdown-link">
          欢迎您 {{this.username}}<i class="el-icon-arrow-down el-icon--right"></i>
        </span>
        <el-dropdown-menu slot="dropdown">
          <el-dropdown-item command="buildNew">新建简历</el-dropdown-item>
          <el-dropdown-item command="saveData">保存简历</el-dropdown-item>
          <el-dropdown-item command="logOut" divided>退出登录</el-dropdown-item>
        </el-dropdown-menu>
      </el-dropdown>
    </div>

  </div>
</template>
<script>
export default {
  props: ['currentUser'],
  created(){
    setInterval(() => {
      if(this.currentUser){
      this.username = this.currentUser.username;
      }
    },1000)
  },
  data(){
    return{
      username: ''
    }

  },
  methods:{
    handleCommand(command) {
      if(command==='buildNew'){
        this.buildNew();
      }else if(command==='saveData'){
        this.saveData();
      }else if(command==='logOut'){
        this.logOut();
      }
    },
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
  >.headButton {
    >button {
      padding: 8px 12px;
    }
    >.menu {
      cursor: pointer;
    }
  }
  
}
</style>

