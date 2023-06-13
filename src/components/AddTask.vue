<template>
    <form @submit="onSubmit" class="add-form">
        <div class = "form-control">
            <label>Termin: </label>
            <input type="text" v-model="text" name="text" placeholder="Termin hinzufügen"/>
        </div>
        <div class = "form-control">
          <label>Datum: </label>
          <input type="date" v-model="date" name="date"/>
        </div>
        <div class = "form-control">
          <label>Uhrzeit: </label>
          <input type="time" v-model="time" name="time"/>
           <br>
          <label>Ganztägig:</label>
          <input type="checkbox" v-model="fullday" name="fullday">
        </div>
        <div class = "form-control">
            <label>Beschreibung: </label>
            <input type="text" v-model="description" name="description" placeholder="Beschreibung hinzufügen">
        </div>
      <input type = "submit" value="Termin speichern" class="btn btn-block"/>
    </form>
</template>

<script>
let index = 4;
export default {
    name : 'AddTask',
    data() {
        return {
            text: '',
            date: '',
            time: '',
            description: ''
        }
    },
    methods:{
        onSubmit(e){
            e.preventDefault()
            if(!this.text){
                alert('Bitte Termin eingeben')
                return
            }
            if (!this.date){
              alert('Bitte Datum eingeben')
              return
            }
            if(!this.time && !this.fullday){
                alert('Bitte Uhrzeit eingeben')
                return
            }
            else if(this.fullday){
              this.time = "Ganztägig"
            }
            const newTask = {
                //id: Math.floor(Math.random()*10000),
                id: index++,
                text: this.text,
                date: this.date,
                time: this.time,
                description: this.description,
                show: null,
            }
            console.log(newTask)
            this.$emit('add-task', newTask)
            this.$emit('task-saved')
            this.text = ''
            this.date = ''
            this.time = ''
            this.description = ''
        },
    }
}
</script>
<style>
form {
  padding: 10px;
  margin: 10px;
  display: flex;
  justify-content: space-between;
  background-color: #f0f0f0;
  margin-left: 10%;
  margin-right: 10%;
}
</style>