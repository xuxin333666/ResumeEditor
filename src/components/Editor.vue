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
      <li class="objectClass" v-bind:class="{action: index === 0}">
        <objectEditor v-bind:objectData="resume.personal" v-bind:label="{name:'姓名',age:'年龄',city:'城市'}" v-bind:title="'个人信息'"/>
      </li>
      <li class="arrClass" v-bind:class="{action: index === 1}">
        <arrEditor v-bind:arrData="resume.workMain" v-bind:label="{company:'公司',workContent:'工作经历'}" v-bind:title="'工作经历'"  v-bind:Textarea="['workContent']"/>
      </li>
      <li class="arrClass" v-bind:class="{action: index === 2}">
        <arrEditor v-bind:arrData="resume.stady" v-bind:label="{startDate:'起始日期',school:'学校',degreeAndProfession:'学位/专业',stadyHistory:'在校经历'}" v-bind:title="'在校经历'"  v-bind:Textarea="['stadyHistory']"/>
      </li>
      <li class="arrClass" v-bind:class="{action: index === 3}">
        <arrEditor v-bind:arrData="resume.project" v-bind:label="{project:'项目名称',projectHistory:'项目内容',learn:'学到了?'}" v-bind:title="'项目经历'"  v-bind:Textarea="['projectHistory','learn']"/>
      </li>
      <li class="arrClass" v-bind:class="{action: index === 4}">
        <arrEditor v-bind:arrData="resume.prize" v-bind:label="{prizeDate:'获奖时间',prizeName:'奖项名称'}" v-bind:title="'获奖情况'"  v-bind:Textarea="[]"/>
      </li>
      <li class="objectClass" v-bind:class="{action: index === 5}">
        <objectEditor v-bind:objectData="resume.contact" v-bind:label="{phone:'电话',wechat:'微信',email:'电子邮箱',guthub:'Github'}" v-bind:title="'联系方式'"/>
      </li>
    </ul>
  </div>
</template>
<script>
import objectEditor from './objectEditor'
import arrEditor from './arrEditor'
export default {
  components: {
    objectEditor,
    arrEditor
  },
  props:['resume'],
  data(){
    return {
      index: 0,
      icon: ['id-card-5','worklinemtui','185072bookreadstreamline','wodexiangmu01','jiangbei','Phone']
    }
  },
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
        padding: 16px 12px;
        width: 32px;
        height: 32px;
      }    
    }
  }
  .editor>.content {
    width: 100%;
    overflow: auto;
    >li {
      padding: 32px;
      display: none;
      &.action {
        display: block;
      }
      &.objectClass {
        width: 75%;
        >.objectEditor>.objectEditor {
          padding-top: 22px;
        }
      }
      >.arrEditor>.arrEditor {
        >.button {
          margin-top: 22px;
        }
        >.container {
          width: 85%;
          position: relative;
          padding-top: 22px;
          >.el-button.remove {
            position: absolute;
            top: 50%;
            transform: translateY(-50%);
            left: 103%;
          }
        }
        .el-form-item__label {
          text-align: left;
        }
      }    
    }
  }
</style>