<template>
  <div class="container">
    <Header title="Task Tracker"/>
    <AddTask @add-task="addTask"/>
    <Tasks @toggle-reminder="toggleReminder"
           @delete-task="deleteTask"
           :tasks="tasks"/>
  </div>
</template>

<script>
import Header from './components/Header.vue'
import Tasks from './components/Tasks.vue';
import AddTask from './components/AddTask.vue';

export default {
  name: 'App',
  components: {
    Header,
    Tasks,
    AddTask
  },
  data() {
    return {
      tasks: [], // Initialize as an array
    }
  },

  methods: {
    addTask(task) {
      // Ensure each new task has a unique ID
      const newTask = { id: Date.now(), ...task }; 
      this.tasks = [...this.tasks, newTask]; // Add the new task to the array
    },

    deleteTask(id) {
      if (confirm('Are you sure?')) {
        this.tasks = this.tasks.filter((task) => task.id !== id); // Remove task by ID
      }
    },
    
    toggleReminder(id) {
      this.tasks = this.tasks.map((task) =>
        task.id === id ? { ...task, reminder: !task.reminder } : task
      );
    },
  },
  
  created() {
    this.tasks = [
      {
        id: 1,
        text: 'Doctors Appointment',
        day: 'October 1st at 2:30PM',
        reminder: true,
      },
      {
        id: 2,
        text: 'Meeting with client',
        day: 'October 2nd at 10:00AM',
        reminder: false,
      },
      {
        id: 3,
        text: 'Lunch with friends',
        day: 'October 3rd at 1:00PM',
        reminder: true,
      }
    ];
  }
}
</script>


<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap');

* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: 'Poppins', sans-serif;
}

.container {
  max-width: 500px;
  margin: 30px auto;
  overflow: auto;
  min-height: 300px;
  border: 1px solid steelblue;
  padding: 30px;
  border-radius: 5px;
}

.btn {
  display: inline-block;
  background: #000;
  color: #fff;
  border: none;
  padding: 10px 20px;
  margin: 5px;
  border-radius: 5px;
  cursor: pointer;
  text-decoration: none;
  font-size: 15px;
  font-family: inherit;
}

.btn:focus {
  outline: none;
}

.btn:active {
  transform: scale(0.98);
}

.btn-block {
  display: block;
  width: 100%;
}
</style>
