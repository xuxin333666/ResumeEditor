<template>
  <div>
    <h3 class="logo">VueResumer</h3>
    <div class="headButton">
      <el-button @click="preview" type="primary" round>预览</el-button>
      <el-dropdown  @command="handleCommand" class="menu">
        <span class="el-dropdown-link">
          欢迎您 {{this.username}}<i class="el-icon-arrow-down el-icon--right"></i>
        </span>
        <el-dropdown-menu slot="dropdown" class="tab">
          <el-dropdown-item command="buildNew">
            <svg class="icon" aria-hidden="true">
                <use xlink:href="#icon-xinjian"></use>
              </svg>
            新建简历</el-dropdown-item>
          <el-dropdown-item command="saveData">
            <svg class="icon" aria-hidden="true">
                <use xlink:href="#icon-save"></use>
              </svg>            
            保存简历</el-dropdown-item>
          <el-dropdown-item command="logOut" divided>
            <svg class="icon" aria-hidden="true">
                <use xlink:href="#icon-dengchu"></use>
              </svg>            
            退出登录</el-dropdown-item>
        </el-dropdown-menu>
      </el-dropdown>
    </div>

  </div>
</template>
<script>
export default {
  props: ['currentUser'],
  created(){
    this.getUsername();
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
    },
    getUsername(){
      let time1 = setInterval(() => {
        if(this.currentUser){
          this.username = this.currentUser.username;
          clearTimeout(time1)
        }
      },1000)
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
.tab>li {
  >svg.icon {
    width: 18px;
    height: 18px;
    fill: #589bf7;
    margin-right: 5px;
  }
}
</style>

