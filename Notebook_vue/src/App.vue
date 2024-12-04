<template>
  <div id="app" class="notebook">
    <Sidebar
      :notes="notes"
      :searchTerm="searchTerm"
      :selectedNoteIndex="selectedNoteIndex"
      @selectNote="selectNote"
      @deleteNote="deleteNote"
      @addNote="addNote"
      @updateSearchTerm="updateSearchTerm"
    />
    <Editor
      v-if="selectedNoteIndex !== null"
      :text="notes[selectedNoteIndex].text"
      @updateText="updateNoteText"
    />
  </div>
</template>

<script>
import Sidebar from "./components/Sidebar.vue";
import Editor from "./components/Editor.vue";

export default {
  components: { Sidebar, Editor },
  data() {
    return {
      notes: [], // Список заметок
      selectedNoteIndex: null, // Индекс выбранной заметки
      searchTerm: "", // Поисковый запрос
    };
  },
  methods: {
    // Добавление заметки
    addNote() {
      const title = prompt("Введите название заметки:", "Новая заметка");
      if (title) {
        this.notes.push({ title, text: "" });
        this.selectedNoteIndex = this.notes.length - 1;
      }
    },
    // Удаление заметки
    deleteNote(index) {
      this.notes.splice(index, 1);
      // Корректируем индекс выбранной заметки
      if (this.selectedNoteIndex === index) {
        this.selectedNoteIndex = null;
      } else if (this.selectedNoteIndex > index) {
        this.selectedNoteIndex -= 1;
      }
    },
    // Выбор заметки
    selectNote(index) {
      this.selectedNoteIndex = index;
    },
    // Обновление текста заметки
    updateNoteText(newText) {
      if (this.selectedNoteIndex !== null) {
        this.notes[this.selectedNoteIndex].text = newText;
      }
    },
    // Обновление поискового запроса
    updateSearchTerm(term) {
      this.searchTerm = term;
    },
  },
};
</script>

<style>
.notebook {
  display: flex;
  height: 100vh;
}
.sidebar {
  width: 250px; 
  background: #333;
  color: #fff;
  padding: 10px;
  box-sizing: border-box;
}
.editor {
  flex: 1; 
  padding: 20px;
  box-sizing: border-box;
  background: #f9f9f9;
}
.sidebar ul {
  list-style: none;
  padding: 0;
  margin: 0;
}
.sidebar li {
  padding: 10px;
  margin: 5px 0;
  background: #444;
  border-radius: 5px;
  cursor: pointer;
  display: flex;
  justify-content: space-between;
  align-items: center;
  color: #fff;
}

.sidebar li.active {
  background: #555;
}

.sidebar li:hover {
  background: #666;
}

.sidebar li button {
  background: #2e8b57;
  color: #fff;
  border: none;
  border-radius: 5px;
  padding: 5px 10px;
  cursor: pointer;
}

.sidebar li button:hover {
  background: #3cb371;
}

.sidebar button {
  background: #2e8b57;
  color: #fff;
  border: none;
  border-radius: 5px;
  padding: 10px;
  width: 100%;
  margin-top: 10px;
  cursor: pointer;
  font-size: 16px;
}

.sidebar button:hover {
  background: #3cb371;
}
</style>

