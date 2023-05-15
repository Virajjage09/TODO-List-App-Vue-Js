<template>
  <form @submit="onSubmit" class="add-form">
    <div class="form-control">
      <label>TODO</label>
      <input type="tex" v-model="text" name="text" placeholder="Add TODO" />
    </div>
    <div class="form-control">
      <label>Day & Time</label>
      <input type="tex" v-model="day" name="day" placeholder="Add Day & Time" />
    </div>
    <div class="form-control form-control-check">
      <label>Set Reminder</label>
      <input type="checkbox" v-model="reminder" name="reminder" />
    </div>
    <input type="submit" value="Save TODO" class="btn" />
  </form>
</template>

<script>
export default {
  name: 'AddTask_View',
  data() {
    return {
      text: '',
      day: '',
      reminder: false
    }
  },
  methods: {
    onSubmit(e) {
      e.preventDefault()

      if (!this.text) {
        alert('Please add Task')
        return
      }

      const task = {
        //id: Math.floor(Math.random() * 100000),
        text: this.text,
        day: this.day,
        reminder: this.reminder
      }

      //console.log('new task', task)
      this.$emit('add-task', task)

      this.text = ''
      this.day = ''
      this.reminder = false
    }
  }
}
</script>

<style scoped>
.add-form {
  margin-bottom: 40px;
}

.form-control {
  margin: 20px 0;
}

.form-control label {
  display: block;
}

.form-control input {
  width: 100%;
  height: 40px;
  margin: 5px;
  padding: 3px 7px;
  font-size: 17px;
}

.form-control-check {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.form-control-check label {
  flex: 1;
}

.form-control-check input {
  flex: 2;
  height: 20px;
}

.btn {
  background-color: blue;
  color: white;
}
</style>