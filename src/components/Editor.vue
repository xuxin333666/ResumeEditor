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
        <objectEditor :objectData="resume.personal" :title="'个人信息'" :Textarea="['自我简述']" :placeholderStr="placeholderStr"/>
      </li>
      <li class="arrClass" :class="{action: index === 1}">
        <arrEditor :arrData="resume.workMain" :title="'工作经历'"  :Textarea="['工作经历']" :placeholderStr="placeholderStr"/>
      </li>
      <li class="arrClass" :class="{action: index === 2}">
        <arrEditor :arrData="resume.stady" :title="'在校经历'"  :Textarea="['在校经历']" :placeholderStr="placeholderStr"/>
      </li>
      <li class="arrClass" :class="{action: index === 3}">
        <arrEditor :arrData="resume.project" :title="'项目经历'"  :Textarea="['项目内容','学到了？']" :placeholderStr="placeholderStr"/>
      </li>
      <li class="arrClass" :class="{action: index === 4}">
        <arrEditor :arrData="resume.prize" :title="'获奖情况'" :Textarea="[]" :placeholderStr="placeholderStr"/>
      </li>
      <li class="objectClass" :class="{action: index === 5}">
        <objectEditor :objectData="resume.contact"  :title="'联系方式'" :Textarea="[]" :placeholderStr="placeholderStr"/>
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
      icon: ['id-card-5','worklinemtui','185072bookreadstreamline','wodexiangmu01','jiangbei','Phone'],
      placeholderStr: {
        '姓名': '填写姓名（必填项）',
        '自我简述': '一句话介绍自己（必填项）',
        '年龄': 'XX岁（必填项）',
        '城市': '填写所在地或意向前往的城市（必填项）',
        '工作时间': '日期格式建议用：2XXX.X.X-2XXX.X.X',
        '公司': '全称或简称均可',
        '职位': '请填写详细职位',
        '工作经历': '按实填写即可',
        '起始日期': '日期格式建议用：2XXX.X.X-2XXX.X.X',
        '学校': '填写毕业证上的学校名称',
        '学位/专业': '填写毕业证上的专业名称（若有）',
        '在校经历': '按实填写即可',
        '项目名称': '按实填写即可',
        "项目内容": '简要描述项目内容，使用的技术等',
        '获奖时间': '日期格式建议用：2XXX.X.X',
        '奖项名称': '荣誉证书、竞赛获奖证书、奖学金等',
        "电话": '建议写成易于拨打的形式，如：185-5555-5555（必填项）',
        "微信": '按实填写即可（必填项）',
        "电子邮箱": '主流邮箱产品如@163.com/@qq.com/@sina.com皆可（必填项）',
        "GitHub": '建议不用填写协议名称节省空间（必填项）'
      }
    }
  },
}
</script>

<style lang=scss>
  .editor>.label {
    width: 100px;
    height: 100%;
    background: #589bf7;
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
  .editor>.content:after {
    content: '';
    position: absolute;
    width: 100%;
    height: 100%;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
    background: url('http://p6o0v7chj.bkt.clouddn.com/%E6%96%87%E8%89%BA%E8%83%8C%E6%99%AF.jpg') no-repeat;
    background-size: cover;
    background-position: right bottom;
    opacity: 0.5;
    z-index: -1;
  }
  .editor>.content {
    width: 100%;
    height: 100%;
    overflow: auto;
    position: relative;
    >li {
      padding: 32px;
      display: none;
      &.action {
        display: block;
      }
      &.objectClass {
        width: 85%;
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