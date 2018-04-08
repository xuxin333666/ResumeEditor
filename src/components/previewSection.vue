<template>
    <section :class="arrData.className">
        <h2 v-if="(!(arrData instanceof Array)) || (filter(arrData) && epmty === false)" class="title">{{title}}</h2>
        <ul class="content" v-for="items in filter(arrData)" :key="items.key">
            <li class="list" v-for="(value,key) in items" :key="key.key">{{key}}:{{value}}</li>
        </ul>
    </section>
</template>
<script>
export default {
    props:['arrData','title'],
    data(){
        return {
            epmty: true
        }
    },
    methods: {
        filter(arr){
            if(arr instanceof Array){
                return this.isEpmty(arr)
            }else{
                return [arr];
            }
        },
        isEpmty(arr){
            arr = arr.map(value => {
                var obj = {};
                for (var key in value ){
                    if(value[key]){
                        obj[key] = value[key];
                        this.epmty = false;
                    }
                }
                return obj;
            })
            return arr;
        }
    }
}
</script>

