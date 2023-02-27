<template>
    <button @click ="onClick()" class="btn">Termin hinzufügen</button>
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