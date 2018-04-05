<template>
  <div class="editor">
    <ul class="label">
      <li class="items" v-for=" i in [0,1,2,3,4,5]" v-bind:key="i" v-bind:class="{action: index === i}" v-on:click=" index = i ">
        <svg class="icon" aria-hidden="true">
          <use :xlink:href="`#icon-${icon[i]}`"></use>
        </svg>
      </li>
    </ul>
    <div class="content">tab1</div>
  </div>
</template>
<script>
export default {
  data(){
    return {
      index: 1,
      icon: ['id-card-5','worklinemtui','185072bookreadstreamline','wodexiangmu01','jiangbei','Phone']
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
</style>