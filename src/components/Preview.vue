<template>
  <div>
    <header>
      <div class="headerBg">
        <form @submit.prevent="upLoadPhoto" action="">
          <input type="file" id="photoFileUpload"/>
          <input type="submit" value="上传头像"> 
          <img class="avatar" :src="avatar.url" alt="">
        </form>
      </div>
    </header>
    <Section v-for="items in arrDataCt" :key="items.key" :title="items.title" :arrData="items.arrData" :class="items.className"/>
    <footer></footer>
  </div>
</template>
<script>
import Section from './previewSection'
export default {
  props:['resume','avatar'],
  data(){
    return {
      arrDataCt: [
        {
          title: '个人信息',
          arrData: this.resume.personal,
          className: 'personal'
        },
        {
          title: '工作经历',
          arrData: this.resume.workMain,
          className: 'workMain'
        },
        {
          title: '学习经历',
          arrData: this.resume.stady,
          className: 'stady'
        },
        {
          title: '项目经历',
          arrData: this.resume.project,
          className: 'project'
        },
        {
          title: '获奖情况',
          arrData: this.resume.prize,
          className: 'prize'
        },
        {
          title: '联系方式',
          arrData: this.resume.contact,
          className: 'contact'
        }
      ]
    }
  },
  components: {
    Section
  },
  methods: {
    upLoadPhoto(){
      this.$emit('upLoadPhoto')
    }
  }
}
</script>

<style lang=scss>
.preview {
  header {
    width: 100%;
    height: 30%;
    overflow: hidden;
    >.headerBg {
      width: 100%;
      height: 55%;
      position: relative;
      background: #589bf7;
    }
    >.headerBg:after {
      content: '';
      position: absolute;
      top: 100%;
      border-bottom: 100px solid white;
      border-left: 1000px solid white;
      border-right: 1000px solid #589bf7;
      border-top: 100px solid #589bf7;
    }
  } 
  >footer {
    width: 280px;
    height: 4%;
    position: absolute;
    right: 0;
    bottom: 0;
    background: #589bf7;
  }  
  >footer:before {
    content: '';
    position: absolute;
    bottom: 100%;
    border-top: 25px solid white;
    border-right: 140px solid white;
    border-left: 140px solid #589bf7;
    border-bottom: 25px solid #589bf7;
  }
}
</style>