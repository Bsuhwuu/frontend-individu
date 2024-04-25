<template>
  <div>
    <h2>Edit Catatan</h2>
    <input type="text" v-model="editedNote">
    <button @click="editNote">Simpan</button>
  </div>
</template>

<script>
import { defineComponent, ref } from 'vue';
import { useNoteStore } from '@/store/store';

export default defineComponent({
  props: ['noteIndex'],
  setup(props) {
    const noteStore = useNoteStore();
    const editedNote = ref(noteStore.notes[props.noteIndex]);

    const editNote = () => {
      if (editedNote.value.trim() !== '') {
        noteStore.editNote({ index: props.noteIndex, newNote: editedNote.value });
      }
    };

    return {
      editedNote,
      editNote,
    };
  },
});
</script>
