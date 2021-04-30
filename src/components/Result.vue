<template>
  <div>
    <p>
      У вас правильных ответов : {{ $props.correct }}

      из {{ $props.length }}
    </p>
  </div>
</template>

<script>
export default {
  props: {
    correct: Number,
    length: Number,
  },
};
</script>
