<template>
  <AddTask v-show="showAddTask" @add-task="addTask"/>
  <Tasks @toggle-reminder="toggleReminder" @delete-task="deleteTask" :tasks="tasks"/>
</template>
<script>
import Tasks from '../components/Tasks.vue'
import AddTask from '../components/AddTask.vue'

export default {
  name: 'Home',
  components: {
    Tasks,
    AddTask
  },
  props:{
    showAddTask : Boolean
  },
  data() {
    return {
    tasks : []
    }
  },
  methods:{
    addTask(task) {
      this.tasks = [ ...this.tasks, task]
    },
    deleteTask(id) {
      this.tasks = this.tasks.filter((task) => {
        return task.id !== id
        })
    },
    toggleReminder(id){
      this.tasks = this.tasks.map((task) => task.id === id ? { ...task, reminder: !task.reminder} : task)
    }
  },
  created() {
    this.tasks = [
        {
          id: 1,
          text: "Finish Vue",
          reminder: true,
          day : "Sep 14 at 12:00am"
        },
        {
          id: 2,
          text: "Learn more technical analysis",
          reminder: true,
          day : "Oct 14 at 12:00am"
        },
        {
          id: 3,
          text: "Get Fit",
          reminder: false,
          day : "Nov 14 at 12:00am"
        }
    ]
  }
}
</script>
