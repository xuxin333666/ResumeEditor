<template>
  <div>
    <header>
      <div class="headerBg">
        <div class="avatarCt">
          <input @change="upLoadPhoto" type="file" accept="image/*" id="photoFileUpload"/>
          <img class="avatar" :src="avatar.url" alt="">
          <div class="hover">
            <svg class="icon" aria-hidden="true">
              <use xlink:href="#icon-shumajiadian"></use>
            </svg>
          </div>
        </div>
      </div>
    </header>
    <Section v-for="items in arrDataCt" :key="items.key" :ArrData="items"/>
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
          className: 'personal',
          icon: {
            '年龄': 'heart',
            '城市': 'City'
          }
        },
        {
          title: '工作经历',
          arrData: this.resume.workMain,
          className: 'workMain',
          titleIcon: 'worklinemtui'
        },
        {
          title: '学习经历',
          arrData: this.resume.stady,
          className: 'stady',
          titleIcon: '185072bookreadstreamline'
        },
        {
          title: '项目经历',
          arrData: this.resume.project,
          className: 'project',
          titleIcon: 'wodexiangmu01'
        },
        {
          title: '获奖情况',
          arrData: this.resume.prize,
          className: 'prize',
          titleIcon: 'jiangbei'
        },
        {
          arrData: this.resume.contact,
          className: 'contact',
          icon: {
            '电话': 'Phone',
            '微信': 'aui-icon-weichat',
            '电子邮箱': 'dianziyoujianemail65',
            'GitHub': 'github'
      
          }
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
    height: 25%;
    overflow: hidden;
    >.headerBg {
      width: 100%;
      height: 70%;
      position: relative;
      background: #589bf7;
      >.avatarCt {
        z-index: 1;
        position: absolute;
        top: 28%;
        right: 10%; 
        width: 16%;
        height: 80%;
        min-width: 80px;
        min-height: 100px;
        background: url('http://p6o0v7chj.bkt.clouddn.com/avatar.jpg') no-repeat;
        background-size: cover;
        background-position: center bottom;
        >input {
          z-index: 4;
          opacity: 0;
        }
        >.avatar {
          z-index: 3;
        }
        >.avatar,>input,>.hover {
          cursor: pointer;
          position: absolute;
          width: 100%;
          height: 100%;
          left: 0;
          top: 0;
        }
        >.hover>svg.icon {
          display: none;
            width: 45%;
            height: 45%;
            position: absolute;
            left: 50%;
            top: 50%;
            transform: translate(-50%,-50%);
            fill: white;
        }
      }
      >.avatarCt:hover>.hover {
          background: #00c091;
          opacity: 0.3;
          >svg.icon {
            display: block;
          }
      }
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
  >section {
    width: 55%;
    >.title {
      margin: 10px 0;
      padding: 6px 20px;
      width: 250px;
      display: flex;
      align-items: center;
      font-size: 16px;
      background: #589bf7;
      color: white;
      >svg.icon {
        fill: white;
      }
    }
    >.content {
      display: flex;
      flex-wrap: wrap;
      border-bottom: 2px dotted #ccc;
      >.list {
        display: flex;
        align-items: center;
        padding: 6px 0 6px 20px;
        font-size: 14px;
      }
      >.list:nth-child(4) {
        width: 100%;
      }
    }
    svg.icon {
      fill: #589bf7;
      width: 25px;
      height: 25px;
      margin-right: 10px;
    }
  }
  >section.personal {
    order: 2;
    width: 40%;
    >.title {
      padding-left: 0;
      padding-right: 0;
      width: 100%;
      background: unset;
      color: #888;
    }
    >.content {
      flex-direction: column;
      border: none;
      >.list {
        padding: 15px 0 10px 0;
        border-bottom: 2px dotted #ccc;
      }
      >.list:first-child {
        color: white;
        font-size: 26px;
        position: absolute;
        top: 60px;
        left: 0;
        margin-left: 50px;
        border-bottom: none;
      }
      >.list:nth-child(2) {
        color: white; 
        position: absolute;
        top: 68px;   
        left: 0;
        margin-left: 120px;  
        border-bottom: none;
      }
    }
  }
  >section.workMain {
    order: 1;
  }
  >section.stady {
    order: 3;
  }
  >section.project {
    order: 5;
  }
  >section.prize {
    order: 6;
  }
  >section.contact {
    order: 4;
    margin-top: -74px;
    width: 40%;
    >.content {
      flex-direction: column;
      border: none;
      >.list {    
        padding: 15px 0 10px 0;
        border-bottom: 2px dotted #ccc;
      }
    }
  }
}
</style>