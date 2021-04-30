<template>
  <div id="app">
    <h1>Tasks</h1>
    <hr />
    <Timer></Timer>
    <ShowTasks :index="index" :tasks="tasks" v-if="show" />

    <div v-else>
      <textarea name="" id="" cols="30" rows="10" v-model="tasks"></textarea>
      <button v-on:click="parse">Start</button>
    </div>
  </div>
</template>

<script>
import ShowTasks from "./components/ShowTasks.vue";
import Timer from "./components/Timer";
export default {
  name: "App",

  components: { ShowTasks, Timer },

  data() {
    return {
      show: false,
      tasks: "",
      index: 0,
    };
  },

  methods: {
    parse() {
      this.tasks = this.tasks.split("\n").map((task) => task.split(","));
      console.log(this.tasks);
      this.show = true;
    }, // парсим строку в двухмерный массив
  },
};
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #152297;
  margin-top: 60px;
}
</style>
