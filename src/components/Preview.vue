<template>
  <div>
    <Section v-for="items in arrDataCt" :key="items.key" :title="items.title" :arrData="items.arrData" :class="items.className"/>
  </div>
</template>
<script>
import Section from './previewSection'
export default {
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
  props:['resume'],
  components: {
    Section
  }
}
</script>

<style lang=scss>
</style>