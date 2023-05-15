<template>
    <div v-show="showAddTask">
        <Add_Task_View @add-task="addTask" />
    </div>
    <Tasks_View @toggle-reminder="toggleReminder" @delete-task='deleteTask' :tasks="tasks" />
</template>

<script>
import Tasks_View from '../components/Tasks_View.vue';
import Add_Task_View from '../components/AddTask_View.vue'

export default {
    name: 'Home_View',
    props: {
        showAddTask: Boolean
    },
    components: {
        Tasks_View,
        Add_Task_View,
    },
    data() {
        return {
            tasks: [],
        }
    },
    methods: {
    async deleteTask(id) {
      console.log('Delete Task', id)
      if (confirm('You sure you want to Delete the Task')) {
        const response = await fetch(`http://localhost:5000/tasks/${id}`, {
          method: 'DELETE',
          headers: {
            'Content-type': 'application/json',
          }
        })
        response.status === 200 ?
          (this.tasks = this.tasks.filter((task) => task.id !== id))
          : alert('Unable to delete')
      }
    },
    async toggleReminder(id) {
      console.log('Toggle Reminder', id)
      const taskToToggle = await this.fetchTask(id)
      //const updateTask = { ...taskToToggle, reminder: !taskToToggle.reminder }
      taskToToggle.reminder = !taskToToggle.reminder

      console.log('Updated Task',JSON.stringify(taskToToggle))

      const response = await fetch(`http://localhost:5000/tasks/${id}`, {
        method: 'PUT',
        headers: {
          'Content-type': 'application/json',
        },
        body: JSON.stringify(taskToToggle)
      })

  
    

      const data = await response.json()

      this.tasks = this.tasks.map((task) => task.id === id ? { ...task, reminder: data.reminder } : task)
      // response.status === 200 ?
      //   (this.tasks = this.tasks.map((task) => task.id === id ? { ...task, reminder: data.reminder } : task))
      //   : alert('Unable to update the task')
    },
    async addTask(task) {
      const response = await fetch('http://localhost:5000/tasks', {
        method: 'POST',
        headers: {
          'Content-type': 'application/json',
        },
        body: JSON.stringify(task)
      })
      const data = await response.json()
      console.log('add task res', data)

      this.tasks = [...this.tasks, task]
    },
    async fetchTasks() {
      const response = await fetch('http://localhost:5000/tasks')
      const data = await response.json()
      return data
    },
    async fetchTask(id) {
      console.log('task', id)
      const response = await fetch(`http://localhost:5000/tasks/${id}`)
      const data = await response.json()
      console.log('single task res', data)
      return data
    }
  },
  async created() {
    // this.tasks = [
    //   {
    //     id: 1,
    //     text: 'Doctor Appointment',
    //     day: 'March 1st at 10.00 AM',
    //     reminder: true
    //   },
    //   {
    //     id: 2,
    //     text: 'Play Cricket',
    //     day: 'March 1st at 05.00 PM',
    //     reminder: false
    //   },
    //   {
    //     id: 3,
    //     text: 'Go to MacD',
    //     day: 'March 1st at 09.00 PM',
    //     reminder: true
    //   }

    // ]
    this.tasks = await this.fetchTasks()
  },
}
</script>