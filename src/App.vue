<template>
  <div class="container">
    <Header_View @toggle-add-task="toggleAddTask" title="TODOs List" :showAddTask=showAddTask />
  
    <router-view :showAddTask="showAddTask"></router-view>    
    <Footer_View />
  </div>
</template>

<script>

import Header_View from './components/Header_View.vue';
import Footer_View from './components/Footer_View.vue';

export default {
  name: 'App',
  components: {
    Header_View,
    Footer_View
},
  data() {
    return {
      showAddTask: false
    }
  },
  methods: {
    toggleAddTask() {
      this.showAddTask = !this.showAddTask
    },
    
  },

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
  border: 1px solid rgb(101, 52, 2);
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
