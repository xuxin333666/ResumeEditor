<template>
    <div class="arrEditor">
        <h2>{{title}}</h2>
        <el-form label-width="75px" class="arrEditor">
            <div class="container" v-for="(items,index) in arrData" :key="items.key">
                <el-form-item v-for="(value,key) in items" :label="key" :key="key" >
                    <el-input :type="  whichIsTextarea(key) ? 'textarea' : 'text'  " :placeholder="placeholderStr[key]" v-model="items[key]"></el-input>
                </el-form-item>
                <el-button @click.prevent="remove(index)" class="remove">删除</el-button>
                <hr>
            </div>
            <el-form-item class="button">
                <el-button @click="add">新增一项</el-button>
                <el-button @click="empty">清空所有</el-button>
            </el-form-item>
        </el-form>  
    </div>        
</template>
<script>
export default {
  props:['arrData','label','title','Textarea','placeholderStr'],
  methods: {
    whichIsTextarea(key){
        return this.Textarea.indexOf(key) !==-1;
    },
    saveArr(){
        var obj ={};
        for (const k in this.arrData[0]) {
                obj[k] = '';               
        }
        return obj
    },
    remove(index) {
      if(this.arrData.length === 1){
            return;
      }
      this.arrData.splice(index, 1)
    },
    add(){    
      this.arrData.push(this.saveArr());
    },
    empty(){
        this.arrData.splice(1,this.arrData.length)
        for(var key in this.arrData[0]){
            this.arrData[0][key] = '';
        }
    }
  }
}
</script>

