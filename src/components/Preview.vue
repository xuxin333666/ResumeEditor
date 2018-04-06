<template>
  <div class="preview">
    <section class="personal">
      <h2 class="title">个人信息</h2>
      <ul class="content" v-for="items in filter(resume.personal)" :key="items.key">
        <li class="list" v-for="(value,key) in items" :key="key">{{key}}:{{value}}</li>
      </ul>
    </section>
    <section class="workMain">
      <h2 class="title">工作经历</h2>
      <ul class="content" v-for="items in filter(resume.workMain)" :key="items.key">
        <li class="list" v-for="(value,key) in items" :key="key">{{key}}:{{value}}</li>
      </ul>
    </section>
    <section class="stady">
      <h2 class="title">学习经历</h2>
      <ul class="content" v-for="items in filter(resume.stady)" :key="items.key">
        <li class="list" v-for="(value,key) in items" :key="key">{{key}}:{{value}}</li>
      </ul>
    </section>
  </div>
</template>
<script>
export default {
  props:['resume'],
  methods: {
    filter(arr){
      if(arr instanceof Array){
        return this.isEpmty(arr)
      }else{
        return [arr];
      }
    },
    isEpmty(arr){
      arr = arr.map(value => {
        var obj = {};
        for (var key in value ){
          if(value[key]){
            obj[key] = value[key];
          }
        }
        return obj;
      })
      return arr;
    }
  }
}
</script>

<style lang=scss>
</style>