<template>
    <button @click="onClick" :style="{background:color}" class="btn btn-primary">{{text}}</button>
</template>
<script>
export default {
    name:'Button',
    props:{
         text:String,
         color:String
    },
    emits:['toggle-add-task'],
    methods: {
        onClick(){
            this.$emit("toggle-add-task");
        }
    },
}
</script>