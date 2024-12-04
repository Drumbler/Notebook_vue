<template>
    <li :class="{ active: isActive }">
      <span @click="select">{{ note.title || 'Без названия' }}</span>
      <button @click.stop="deleteNote">Удалить</button>
    </li>
  </template>
  
  <script>
  export default {
    props: {
      note: Object,
      isActive: Boolean,
    },
    methods: {
      select() {
        this.$emit("click");
      },
      deleteNote() {
        this.$emit("delete");
      },
    },
  };
  </script>
  
  <style>
  li {
    display: flex;
    justify-content: space-between;
    padding: 5px;
    cursor: pointer;
  }
  li.active {
    background: #e0e0e0;
  }
  button {
    background: none;
    border: none;
    color: red;
    cursor: pointer;
  }
  </style>
  