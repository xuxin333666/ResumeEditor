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
      height: 60%;
      position: relative;
      background: #589bf7;
      >.avatarCt {
        z-index: 1;
        position: absolute;
        top: 28%;
        right: 10%; 
        width: 14.6%;
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
  >section:first-of-type {
    >section:first-of-type>.content>.list:fist-child {
      position: absolute;
      top: 0;
    }
  }
}
</style>