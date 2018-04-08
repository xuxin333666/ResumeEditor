<template>
    <section :class="ArrData.className">
        <h2 v-if="((!(ArrData.arrData instanceof Array)) || (filter(ArrData.arrData) && epmty === false))&&ArrData.title" class="title">
            <svg v-if="ArrData.titleIcon" class="icon" aria-hidden="true">
                <use :xlink:href="`#icon-${ArrData.titleIcon}`"></use>
            </svg>
            {{ArrData.title}}</h2>
        <ul class="content" v-for="items in filter(ArrData.arrData)" :key="items.key">
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
            this.empty = true;
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

