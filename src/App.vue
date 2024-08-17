<template>
  <div id="app">
    <builder-home />
  </div>
</template>

<script>
import BuilderHome from './views/BuilderHome.vue';

export default {
  name: 'App',
  components: {
    BuilderHome
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
