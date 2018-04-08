<template>
    <section :class="ArrData.className">
        <h2 v-if="((!(ArrData.arrData instanceof Array)) || (filter(ArrData.arrData) && empty === false))&&ArrData.title" class="title">
            <svg v-if="ArrData.titleIcon" class="icon" aria-hidden="true">
                <use :xlink:href="`#icon-${ArrData.titleIcon}`"></use>
            </svg>
            {{ArrData.title}}</h2>
        <ul class="content" v-for="items in filter(ArrData.arrData)" :style="empty?'border:none':''" :key="items.key">
            <li class="list" v-for="(value,key) in items" :key="key.key">
                <svg v-if="ArrData.icon" class="icon" aria-hidden="true">
                    <use :xlink:href="`#icon-${ArrData.icon[key]}`"></use>
                </svg>
            {{value}}</li>
        </ul>
    </section>
</template>
<script>
export default {
    props:['ArrData'],
    data(){
        return {
            empty:  true
        }
    },
    methods: {
        filter(arr){
            if(arr instanceof Array){
                return this.isEmpty(arr)
            }else{
                return [arr];
            }
        },
        isEmpty(arr){
            arr = arr.map(value => {
                var obj = {};
                for (var key in value ){
                    if(value[key]){
                        obj[key] = value[key];
                        this.empty = false;
                    }
                }
                if(Object.keys(obj).length === 0){
                    this.empty = true;
                }
                return obj;
            })
            return arr;
        }
    }
}
</script>

