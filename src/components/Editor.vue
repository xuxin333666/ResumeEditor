<template>
  <div class="editor">
    <ul class="label">
      <li class="items" v-for=" i in [0,1,2,3,4,5]" v-bind:key="i" v-bind:class="{action: index === i}" v-on:click=" index = i ">
        <svg class="icon" aria-hidden="true">
          <use :xlink:href="`#icon-${icon[i]}`"></use>
        </svg>
      </li>
    </ul>
    <ul class="content">
      <li class="personal" v-bind:class="{action: index === 0}">
        <el-form :label-position="'top'" label-width="80px">
          <el-form-item label="姓名">
            <el-input  v-model="personal.name"></el-input>
          </el-form-item>
          <el-form-item label="年龄">
            <el-input v-model="personal.age"></el-input>
          </el-form-item>
          <el-form-item label="城市">
            <el-input v-model="personal.city"></el-input>
          </el-form-item>
        </el-form>
      </li>
      <li v-bind:class="{action: index === 1}">
        <el-form label-width="70px" class="work">
          <div class="container" v-for="(items, index) in workMain" :key="items.key">
            <el-form-item
              :label="'公司'"
              :key="items.key" >
              <el-input v-model="items.company"></el-input>
            </el-form-item>
            <el-form-item label="工作内容" :key="items.key" >
              <el-input type="textarea" v-model="items.workContent"></el-input>
            </el-form-item>
            <el-button @click.prevent="remove(items,index)" class="remove">删除</el-button>
            <hr>
          </div>
          <el-form-item class="button">
            <el-button @click="add()">新增一项</el-button>
            <el-button @click="empty()">清空所有</el-button>
          </el-form-item>
        </el-form>
      </li>
    </ul>
  </div>
</template>
<script>
export default {
  data(){
    return {
      index: 1,
      icon: ['id-card-5','worklinemtui','185072bookreadstreamline','wodexiangmu01','jiangbei','Phone'],
      personal: {
        name: '',
        age: '',
        city: ''
      },
      workMain: [{
        company: '',
        workContent: ''
      }]
    }
  },
  methods: {
    remove(item) {
      var index = this.workMain.indexOf(item)
      if (index !== -1) {
        this.workMain.splice(index, 1)
      }
    },
    add(){
      this.workMain.push({
        company: '',
        workContent: ''
      })
    },
    empty(){
      this.workMain = [{
        company: '',
        workContent: ''
      }]
    }
  }
}
</script>

<style lang=scss>
  .editor>.label {
    width: 100px;
    height: 100%;
    background: black;
    box-shadow: 2px 0 8px rgba(0, 0, 0, 0.2),4px 0 4px rgba(0, 0, 0, 0.2);
    >.items {
      cursor: pointer;
      text-align: center;
      &:hover {
        background: rgba(250, 213, 213, 0.1);
      }
      &.action {
        background: white;
        >svg.icon {
          fill: black;
        }
      } 
      >svg.icon {
        box-sizing: content-box;
        fill: white;
        padding: 12px;
        width: 32px;
        height: 32px;
      }    
    }
  }
  .editor>.content {
    width: 100%;
    overflow: auto;
    >li {
      padding: 16px 32px;
      display: none;
      &.action {
        display: block;
      }
      &.personal {
        width: 75%;
      }
      >.work {
        >.button {
          margin-top: 22px;
        }
        >.container {
          width: 70%;
          position: relative;
          padding-top: 22px;
          >.el-button.remove {
            position: absolute;
            top: 50%;
            transform: translateY(-50%);
            left: 110%;
          }
        }
        .el-form-item__label {
          text-align: left;
        }
      }    
    }
  }
</style>