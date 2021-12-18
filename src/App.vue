<script>
import MacroLastDayTimeLine from "./components/MacroLastDaysTimeline.vue"
export default {
  components: {
    MacroLastDayTimeLine
  }
}
</script>
<template>
  <div id="app">
    <h1>Last Days Timeline</h1>
    <MacroLastDayTimeLine />
  </div>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #fff;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #fff;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>
