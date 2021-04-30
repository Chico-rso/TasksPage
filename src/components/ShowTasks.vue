<template>
  <div>
    <Result
      v-if="isCompleted"
      v-bind:correct="correct"
      v-bind:length="tasks.length"
    ></Result>
    <div v-else>
      <div>{{ tasks[taskIndex][0] }}</div>
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

  methods: {
    loadNextTasks() {
      if (this.tasks.length - 1 == this.taskIndex) {
        this.isCompleted = true;//условия последней задачи
        if (this.userAnswer == this.tasks[this.taskIndex][1]) {
          this.correct++;
        }// счетчик правильных ответов
        return;
      }
      if (this.userAnswer == this.tasks[this.taskIndex][1]) {
        this.correct++;
      }

      console.log(this.userAnswer, this.tasks[this.taskIndex][1]);
      this.userAnswer = "";

      this.taskIndex += 1;// след задача
    },
  },
};
</script>
