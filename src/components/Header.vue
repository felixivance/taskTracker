<template>
    <header>
        <h1>{{title}}</h1>
        <Button :text="showAddTask ? 'Close' : 'Add Task' " @toggle-add-task="$emit('toggle-add-task')" 
        :color="showAddTask ? 'red' : 'green' "/>
    </header>
</template>
<script>
import Button from './Button.vue';

export default {
    name:'headerComponent',
    props:{
        title:{
            type:String,
            default: 'Welcome Felix'
        },
        showAddTask:{
            type:Boolean,default:false
        }
    },
    emits:['toggle-add-task'],
    components:{
        Button
    }
}
</script>
<style scoped>
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
}
</style>