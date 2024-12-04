<template>
    <div class="editor">
      <textarea v-model="localText" @input="updateText"></textarea>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      text: String, // Текущий текст заметки
    },
    data() {
      return {
        localText: this.text, // Локальная копия текста
      };
    },
    watch: {
      // Обновляем локальный текст, если родительский текст изменился
      text(newVal) {
        this.localText = newVal;
      },
    },
    methods: {
      updateText() {
        this.$emit("updateText", this.localText); // Отправляем обновление родителю
      },
    },
  };
  </script>
  

<style>
.editor {
  flex: 1;
  padding: 20px;
  box-sizing: border-box;
  background: #f9f9f9;
  display: flex;
  justify-content: center;
  align-items: center;
  margin: 0;
}

textarea {
  width: 100%;
  max-width: 1200px;
  height: calc(100% - 40px);
  resize: none;
  padding: 10px;
  font-size: 16px;
  box-sizing: border-box;
  border: 1px solid #ccc;
  border-radius: 8px;
  background: #fff;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
  transition: border 0.3s;
}

textarea:focus {
  border-color: #2e8b57;
  outline: none;
}
</style>
