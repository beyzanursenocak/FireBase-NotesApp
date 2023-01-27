<template>
  <button>
    <slot></slot>
  </button>
</template>

<style scoped>
button {
  font: inherit;
  border: 1px solid rgb(32, 51, 114);
  background-color: rgb(32, 51, 114);
  color: white;
  padding: 0.5rem 2rem;
  cursor: pointer;
}

button:hover,
button:active {
  background-color: rgb(9, 24, 73);
  border-color: rgb(9, 24, 73);
}
</style>