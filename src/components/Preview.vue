<template>
  <div>
    <header>
      <div class="headerBg">
        <div class="headerMain">
          <div class="content">
            <p class="name">{{resume.personal.姓名}}<span class="describe">{{resume.personal.自我简述}}</span></p>
          </div>
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
      </div>
    </header>
    <div class="resumeMain">
      <div class="arrData">
        <Section v-for="items in ArrDataCt" :key="items.key" :ArrData="items"/>
      </div>
      <div class="objData">
        <Section v-for="items in ObjDataCt" :key="items.key" :ArrData="items"/>
      </div>
      <footer></footer>
    </div>
  </div>
</template>
<script>
import Section from './previewSection'
export default {
  props:['resume','avatar'],
  created(){
    this.ObjDataCt = [];
    this.ArrDataCt = this.arrDataCt.filter(value => {
      if(value.arrData instanceof Array){
        return value;
      }else{
        this.ObjDataCt.push(value);
      }
    })
  },
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
            '电话': 'phone',
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
      >.headerMain {
        padding: 0 20px;
        display: flex;
        justify-content: space-around;
        align-items: center;
        height: 130%;
        >.content {
          >.name {
            color: white;
            font-size: 32px;
            >.describe {
              margin-left: 15px;
              font-size: 15px;
            }
          }
        }
        >.avatarCt {
          margin-left: 20px;
          position: relative;
          width: 100%;
          height: 100%;
          max-width: 105px;
          max-height: 128px;
          min-width: 80px;
          min-height: 100px;
          background: url('http://p6o0v7chj.bkt.clouddn.com/avatar.jpg') no-repeat;
          background-size: cover;
          background-position: center bottom;
          cursor: pointer;
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
  >.resumeMain {
    margin-top: 20px;
    flex: 1;
    display: flex;
    align-content: space-between;
    flex-wrap: wrap;
    >.arrData {
      width: 68%;
    }
    >.objData {
      width: 32%;
    }
    >footer {
      position: relative;
      width: 100%;
      height: 4%;
      background: #589bf7;
    }  
    >footer:before {
      content: '';
      position: absolute;
      bottom: 100%;
      right: 0;
      border-top: 25px solid white;
      border-right: 80px solid white;
      border-left: 80px solid #589bf7;
      border-bottom: 25px solid #589bf7;
    }
  }
  >.resumeMain section {
    >.title {
      margin: 10px 0;
      padding: 5px 20px;
      width: 220px;
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
      margin-right: 20px;
      display: flex;
      flex-wrap: wrap;
      border-bottom: 2px dotted #ccc;
      >.list {
        min-width: 33%;
        padding: 8px 0 8px 20px;
        font-size: 14px;
      }
      >.list:nth-child(1) {
        white-space: nowrap;
      }
    }
    svg.icon {
      fill: #589bf7;
      width: 25px;
      height: 25px;
      margin-right: 10px;
    }
  }
  >.resumeMain>.objData>section {
    >.title {
      padding: 5px 0;
      width: 100%;
      background: unset;
      color: #888;
    }
    >.content {
      margin-right: 0;
      flex-direction: column;
      border: none;
      >.list {
        display: flex;
        align-items: center;
        width: 100%;
        padding-left: 0;
        border-bottom: 2px dotted #ccc;
      }
    }
  }
  section.personal {
    >.content {
      >.list:first-child {
        display: none;
      }
      >.list:nth-child(2) {
        display: none;
      }
    }   
  }
  section.contact {
    >.content {
      >.list:nth-child(4) {
        font-size: 12px;
      }
    }
  }
}
</style>