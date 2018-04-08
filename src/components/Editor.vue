<template>
  <div>
    <ul class="label">
      <li class="items" v-for=" i in [0,1,2,3,4,5]" :key="i" :class="{action: index === i}" v-on:click=" index = i ">
        <svg class="icon" aria-hidden="true">
          <use :xlink:href="`#icon-${icon[i]}`"></use>
        </svg>
      </li>
    </ul>
    <ul class="content">
      <li class="objectClass" :class="{action: index === 0}">
        <objectEditor :objectData="resume.personal" :title="'个人信息'"/>
      </li>
      <li class="arrClass" :class="{action: index === 1}">
        <arrEditor :arrData="resume.workMain" :title="'工作经历'"  :Textarea="['工作经历']"/>
      </li>
      <li class="arrClass" :class="{action: index === 2}">
        <arrEditor :arrData="resume.stady" :title="'在校经历'"  :Textarea="['在校经历']"/>
      </li>
      <li class="arrClass" :class="{action: index === 3}">
        <arrEditor :arrData="resume.project" :title="'项目经历'"  :Textarea="['项目内容','学到了？']"/>
      </li>
      <li class="arrClass" :class="{action: index === 4}">
        <arrEditor :arrData="resume.prize" :title="'获奖情况'" :Textarea="[]"/>
      </li>
      <li class="objectClass" :class="{action: index === 5}">
        <objectEditor :objectData="resume.contact"  :title="'联系方式'"/>
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
          margin-right: 75px;
          text-align: center;
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