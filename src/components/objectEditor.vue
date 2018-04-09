<template>
    <div class="objectEditor">
        <h2>{{title}}</h2>
        <el-form :label-position="'top'" label-width="80px" class="objectEditor" >
            <el-form-item v-for="(value,key) in objectData" :key="key" :label="key" >
                <el-input :type="  whichIsTextarea(key) ? 'textarea' : 'text'  " :placeholder="placeholderStr[key]" v-model="objectData[key]"></el-input>
            </el-form-item>
        </el-form>
    </div>
</template>
<script>
export default {
  props:['objectData','label','title','Textarea','placeholderStr'],
  methods: {
    whichIsTextarea(key){
        return this.Textarea.indexOf(key) !==-1;
    }
  }
}
</script>

