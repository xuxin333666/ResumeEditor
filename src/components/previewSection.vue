<template>
    <section class="personal">
        <h2 class="title">{{title}}</h2>
        <ul class="content" v-for="items in filter(arrData)" :key="items.key">
            <li class="list" v-for="(value,key) in items" :key="key">{{key}}:{{value}}</li>
        </ul>
    </section>
</template>
<script>
export default {
    props:['arrData','title'],
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
                    }
                }
                return obj;
            })
            return arr;
        }
    }
}
</script>

