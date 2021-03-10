<template>
  <div class="container">
      <DarkModeButton 
        :textColor=" darkMode ? '#fff' : '#1d1d23'"
        @dark-mode-click="darkThemeSwitch"
        :darkMode="darkMode"
      />
      
    <Header title="Task Tracker" @toggle-add-task='toggleAddTask' :showAddTask="showAddTask" />
    <router-view :showAddTask="showAddTask"></router-view>
    <Footer />
  </div>
</template>

<script>
import Header from './components/Header'
import Footer from './components/Footer'
import themeChanger from './theme'
import DarkModeButton from './components/DarkModeButton'

export default {
  name: 'App',
  components: {
    Header,
    Footer,
    DarkModeButton
  },
  data() {
    return {
      showAddTask: false,
      themeChanger: null,
      darkMode: false
    }
  },
  methods: {
    toggleAddTask: function() {
      this.showAddTask = !this.showAddTask
    },
    darkThemeSwitch() {
      this.themeChanger._darkThemeSwitch();
      this.darkMode = !this.darkMode
      console.log(this.darkMode);
    },
  },
  created() {
    this.themeChanger = new themeChanger();
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
