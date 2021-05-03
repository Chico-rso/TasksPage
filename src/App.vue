<template>
  <div id="app">
    <h1>Tasks</h1>
    <hr />
    <div>Timer : {{ currentTime }}</div>
    <br />
    <ShowTasks
      :index="index"
      :tasks="tasks"
      :currentTime="currentTime"
      v-if="show"
    />

    <div v-else>
      <textarea
        @change="activeButton"
        name=""
        id=""
        cols="30"
        rows="10"
        v-model="tasks"
      ></textarea>
      <br />
      <button v-bind:disabled="button" v-on:click="parse">Start</button>
      <div @change="activeButton">
        <input type="radio" value="3" v-model="currentTime" />
        <label for="value"> 3</label>
        <input type="radio" value="45" v-model="currentTime" />
        <label for="value"> 45</label>
        <input type="radio" value="60" v-model="currentTime" />
        <label for="value"> 60</label>
      </div>
    </div>
  </div>
</template>

<script>
import ShowTasks from "./components/ShowTasks.vue";

export default {
  name: "App",

  components: { ShowTasks },

  data() {
    return {
      show: false,
      tasks: "",
      index: 0,
      currentTime: "",
      timer: null,
      button: true,
    };
  },

  methods: {
    parse() {
      this.tasks = this.tasks.split("\n").map((task) => task.split(","));
      console.log(this.tasks);
      this.show = true; // парсим строку в двухмерный массив

      this.timer = setInterval(() => {
        this.currentTime--;
        if (this.currentTime <= 0) {
          clearInterval(this.timer);
        }
      }, 1000); //timer
    },
    activeButton() {
      if (this.tasks.length != 0 && this.currentTime) {
        this.button = false;
      } //условия пока не будет выбраны время таимера и задачи кнопка не активна
    },
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
