<template>
    <div class="sidebar">
      <input
        v-model="localSearchTerm"
        placeholder="Поиск заметок"
        @input="$emit('updateSearchTerm', localSearchTerm)"
      />
      <ul>
        <NoteItem
          v-for="(note, index) in filteredNotes"
          :key="index"
          :note="note"
          :isActive="index === selectedNoteIndex"
          @click="selectNote(index)"
          @delete="deleteNote(index)"
        />
      </ul>
      <button @click="$emit('addNote')">Добавить заметку</button>
    </div>
  </template>
  
  <script>
  import NoteItem from "./NoteItem.vue";
  
  export default {
    components: { NoteItem },
    props: {
      notes: Array,
      searchTerm: String,
      selectedNoteIndex: Number,
    },
    data() {
      return {
        localSearchTerm: this.searchTerm,
      };
    },
    computed: {
      filteredNotes() {
        const term = this.localSearchTerm.toLowerCase();
        return this.notes.filter(
          (note) =>
            note.title.toLowerCase().includes(term) ||
            note.text.toLowerCase().includes(term)
        );
      },
    },
    methods: {
      selectNote(index) {
        const globalIndex = this.notes.indexOf(this.filteredNotes[index]);
        this.$emit("selectNote", globalIndex);
      },
      deleteNote(index) {
        const globalIndex = this.notes.indexOf(this.filteredNotes[index]);
        this.$emit("deleteNote", globalIndex);
      },
    },
  };
  </script>
  
  <style>
  .sidebar {
    width: 300px;
    background: #f4f4f4;
    padding: 10px;
    box-sizing: border-box;
  }
  </style>
  