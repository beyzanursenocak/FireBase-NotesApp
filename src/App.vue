<template>
  <note-comp @note-result="notesList"></note-comp>
  <note-output :results="savedNotes"></note-output>
</template>

<script>
import NoteComp from "./components/Notes/NoteComp.vue";
import NoteOutput from "./components/Notes/NoteOutput.vue";
export default {
  components: {
    NoteComp,
    NoteOutput,
  },
};
</script>

<style>
</style>
