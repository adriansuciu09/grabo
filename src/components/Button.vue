<template>
    <button @click ="onClick()" class="btn">Add Task</button>
</template>

<script>
export default {
    name: 'Button-one',
    methods: {
        onClick() {
            console.log('Clicked')
        }
    }
}
</script>