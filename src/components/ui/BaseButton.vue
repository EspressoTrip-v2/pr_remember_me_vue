<template>
  <button @click="action" :class="mode" :type="type">
    <slot>Submit</slot>
  </button>
</template>

<script>
export default {
  props: {
    action: {
      type: Function,
      required: false,
    },
    mode: {
      type: String,
      required: true,
    },
    type: {
      type: String,
      default: 'button',
    },
  },
};
</script>
<style scoped>
button {
  padding: 0.75rem 1.5rem;
  font-family: inherit;
  background-color: #3a0061;
  border: 1px solid #3a0061;
  color: white;
  cursor: pointer;
}

button:hover,
button:active {
  background-color: #270041;
  border-color: #270041;
}

.flat {
  background-color: transparent;
  color: #3a0061;
  border: none;
}

.flat:hover,
.flat:active {
  background-color: #edd2ff;
}
</style>
