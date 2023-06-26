<template>
  <form @submit="onSubmit" class="add-form">
    <div class="form-control">
      <label>Termin: </label>
      <input type="text" v-model="text" name="text" placeholder="Termin hinzufügen"/>
    </div>
    <div class="form-control">
      <label>Datum: </label>
      <input type="date" v-model="date" name="date"/>
    </div>
    <div class="form-control">
      <label>Uhrzeit: </label>
      <input type="time" v-model="time" name="time"/>
      <br>
      <label>Ganztägig:</label>
      <input type="checkbox" v-model="fullday" name="fullday">
    </div>
    <div class="form-control">
      <label>Beschreibung: </label>
      <input type="text" v-model="description" name="description" placeholder="Beschreibung hinzufügen">
    </div>
    <input type="submit" value="Termin speichern" class="btn btn-block"/>
  </form>
</template>

<script>
import Swal from 'sweetalert2';

function fireAlertSuccess(alertText) {
  Swal.fire({
    icon: 'success',
    title: alertText,
    color: 'black',
    showConfirmButton: true,
    timer: 1500,
  })
}

function fireAlertError(alertText) {
  Swal.fire({
    icon: 'error',
    title: alertText,
    color: 'black',
    showConfirmButton: false,
    timer: 1500,
  })
}

let index = 0;
export default {
  name: 'AddTask',
  data() {
    return {
      text: '',
      date: '',
      time: '',
      description: ''
    }
  },
  methods: {
    onSubmit(e) {
      e.preventDefault()
      if (!this.text) {
        fireAlertError("Bitte Termin eingeben");
        return
      }
      if (!this.date) {
        fireAlertError("Bitte Datum eingeben");
        return
      }
      if (!this.time && !this.fullday) {
        fireAlertError("Bitte Uhrzeit eingeben");
        return
      } else if (this.fullday) {
        this.time = "Ganztägig"
      }
      const newTask = {
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
      fireAlertSuccess("Termin " + this.text + " wurde erfolgreich gespeichert");
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
  font-weight: bold;
  padding: 10px;
  margin: 10px 10%;
  display: flex;
  justify-content: space-between;
  background-color: #f0f0f0;
}
</style>