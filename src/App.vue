<template>
  <div class="container">
    <Header @add-task-btn="handleAddTask" title="Task Manager" :showAddTask="showAddTask"/>
    <div v-show="showAddTask">
      <AddTask @add-task="addTask"/>
    </div>
    <Tasks @toogle-remainder="toogleRemainder" @delete-task="deleteTask" :tasks="tasks"/>
  </div>
</template>

<script>
import Header from './components/Header';
import Tasks from "./components/Tasks";
import AddTask from './components/Addtask'

export default {
  name: "App",
  components: {
    Tasks,
    Header,
    AddTask
  },
  data() {
    return {
      tasks: [],
      showAddTask: false
    }
  },
  created() {
    this.tasks = [{
      id: 1,
      text: "Doctor Appointment",
      day: 'March 1st at 02:30pm',
      remainder: true
    },
      {
        id: 2,
        text: 'Meeting at School',
        day: 'March 2nd at 09:15am',
        remainder: true
      },
      {
        id: 3,
        text: "Family Meeting",
        day: 'March 5th at 2:30pm',
        remainder: false
      }
    ]
  },
  methods: {
    handleAddTask() {
      this.showAddTask = !this.showAddTask
    },
    addTask(task) {
      this.tasks = [...this.tasks, task]
    },

    deleteTask(id) {
      if (confirm('Are you sure you want to delete ? ')) {
        this.tasks = this.tasks.filter(task => task.id !== id)
      }
    },
    toogleRemainder(id) {
      this.tasks = this.tasks.map(task => task.id === id ?
          {...task, remainder: !task.remainder} : task
      )
    }
  }
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap");

* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: "Poppins", sans-serif;
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
