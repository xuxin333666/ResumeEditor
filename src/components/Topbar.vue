<template>
  <div>
    <h3 class="logo">
      <svg class="icon" aria-hidden="true">
        <use xlink:href="#icon-iconfontmojiezuo"></use>
      </svg>      
    VueResumer</h3>
    <el-steps  :stepStatus="stepStatusCTR" process-status="wait" finish-status="success" :active="active" class="stepCt" simple>
      <el-step title="上传头像" icon="el-icon-picture"></el-step>
      <el-step title="编辑简历" icon="el-icon-edit"></el-step>
      <el-step title="保存至云" icon="el-icon-upload"></el-step>
    </el-steps>
    <div class="headButton">
      <el-button @click="preview" type="primary" round>预览</el-button>
      <el-button @click="saveData" type="success" round>保存</el-button>
      <el-button @click="buildNew" type="primary" round>新建</el-button>
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
      <li>
        {{count}}
        <button @click="count=1">test</button>
      </li>
  </div>
</template>
<script>
export default {
  props: ['currentUser','stepStatus','resume'],
  created(){
    this.getUsername();
    setTimeout(()=>{
      this.stepStatusCTR();
      this.$watch('resume',this.resumeEditor, {deep: true})
      this.$watch('stepStatus',this.stepStatusCTR, {deep: true})
    },1500)
  },
  data(){
    return{
      username: '',
      active: 0
    }
  },
 computed: {
      count: {
        get(){
          return this.$store.state.count
        },
        set(){
          return this.$store.commit('increment')
        }
      }
    },
  methods: {
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
    },
    stepStatusCTR(){
      if (this.stepStatus.isUploadPhoto) {
        if(this.stepStatus.isSaveData && this.stepStatus.isEditor){
          this.active = 3;
        }else if(this.stepStatus.isEditor){
          this.active = 2; 
        }else{
          this.active = 1;
        } 
      }
    },
    resumeEditor(){
      this.stepStatus.isSaveData = false;
      this.stepStatus.isEditor = true;
    }
  }
}
</script>
<style lang=scss>
.topbar {
  >.logo {
    width: 33%;
    cursor: default;
    display: flex;
    align-items: center;
    >svg.icon {
      width: 36px;
      height: 36px;
      fill: #589bf7;
    }
  }
  >.stepCt {
    cursor: default;
    padding: 0;
    width:33%;
    min-width: 400px;
    height: 100%;
    background: white;
  }
  >.headButton {
    width: 33%;
    min-width: 400px;
    text-align: right;
    >button {
      padding: 8px 12px;
    }
    >.menu {
      margin-left: 20px;
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

