<template>
    <form @submit="onSubmit" class="add-form">
        <div class = "form-control">
            <label>Termin: </label>
            <input type="text" v-model="text" name="text" placeholder="Termin hinzufügen"/>
        </div>
        <div class = "form-control">
            <label>Tag und Uhrzeit: </label>
            <input type="text" v-model="time" name="time" placeholder="Tag und Uhrzeit hinzufügen"/>
        </div>
        <input type = "submit" value="Termin speichern" class="btn btn-block"/>
    </form>
</template>

<script>

export default {
    name : 'AddTask',
    data() {
        return {
            text: '',
            time: ''
        }
    },
    methods:{
        onSubmit(e){
            e.preventDefault()
            if(!this.text){
                alert('Bitte Termin eingeben')
                return
            }
            if(!this.time){
                alert('Bitte Tag und Uhrzeit eingeben')
                return
            }
            const newTask = {
                id: Math.floor(Math.random()*10000),
                text: this.text,
                time: this.time
            }
            
            console.log(newTask)

            this.$emit('add-task', newTask)
            this.text = ''
            this.time = ''
        }
    }
}
</script>
