<template>
  <div>
    <Result
      v-if="isCompleted"
      v-bind:correct="correct"
      v-bind:length="tasks.length"
    ></Result>
    <div v-else>
      <div>{{ tasks[taskIndex][0] }} =</div>
      <br />
      <input v-model="userAnswer" />
      <button v-on:click="loadNextTasks">Answer</button>
    </div>
  </div>
</template>

<script>
import Result from "./Result";

export default {
  props: {
    tasks: Array,
    index: Number,
    currentTime: [Number, String],
  },
  components: {
    Result,
  },
  data() {
    return {
      userAnswer: "",
      taskIndex: this.$props.index,
      isCompleted: false,
      correct: 0,
    };
  },
  watch: {
    currentTime: function(value) {
      if (value == 0) {
        this.isCompleted = true;
      }
    },
  },

  methods: {
    loadNextTasks() {
      if (this.tasks.length - 1 == this.taskIndex) {
        this.isCompleted = true; //условия последней задачи
        if (this.userAnswer == this.tasks[this.taskIndex][1]) {
          this.correct++;
        } // счетчик правильных ответов
        return;
      }
      if (this.userAnswer == this.tasks[this.taskIndex][1]) {
        this.correct++;
      }

      this.taskIndex += 1; // след задача
    },
  },
};
</script>
