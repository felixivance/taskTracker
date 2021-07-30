<template>
    <div v-for="task in tasks" :key="task">
        <h3>{{task.text}}</h3>
    </div>
</template>
<script>
export default {
    props:{
        tasks:Array
    }
}
</script>