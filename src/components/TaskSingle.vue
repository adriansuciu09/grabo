<template>
<div class="task">
<h3>{{task.text}} </h3>
<p>{{task.date}} </p>
<p>{{task.time}} </p>
<i @click="onDelete(task.id)" class = "fas fa-times"></i>
</div>
</template>

<script>
    export default {
    name: 'TaskSingle',
    props: {
        task: Object
    },
    methods: {
        onDelete(id){
            console.log(id)
            this.$emit('delete-task',id)
        },
    }
    }
</script>

<style>
.task {
    padding: 10px;
    margin: 10px;
    display: flex;
    justify-content: space-between;
    background-color: #f0f0f0;
    margin-left: 10%;
    margin-right: 10%;
}

    
</style>