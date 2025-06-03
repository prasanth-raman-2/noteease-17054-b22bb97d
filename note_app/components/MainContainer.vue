<template>
  <div class="main-container">
    <!-- Search Bar -->
    <div class="search-bar">
      <input
        type="text"
        v-model="searchQuery"
        placeholder="Search notes..."
        aria-label="Search notes"
      />
    </div>

    <!-- Notes List -->
    <div class="notes-list">
      <div
        v-for="note in filteredNotes"
        :key="note.id"
        class="note-card"
        @click="editNote(note)"
      >
        <h3 class="note-title">{{ note.title }}</h3>
        <p class="note-snippet">{{ note.contentSnippet }}</p>
        <div class="tags">
          <span
            v-for="tag in note.tags"
            :key="tag"
            class="tag-label"
          >
            {{ tag }}
          </span>
        </div>
      </div>
    </div>

    <!-- Floating Action Button -->
    <button class="fab" @click="createNote">
      +
    </button>
  </div>
</template>

<script setup>
// PUBLIC_INTERFACE
// MainContainer implements the core layout: search, list, tags, and actions.

import { reactive, computed } from 'vue';

// Sample reactive data; will be replaced with real API/store integration
const state = reactive({
  searchQuery: '',
  notes: [
    {
      id: 1,
      title: 'Sample Note',
      contentSnippet: 'This is a sample content snippet...',
      tags: ['Personal', 'Ideas'],
    },
    {
      id: 2,
      title: 'Work Todo',
      contentSnippet: 'Finish the report by...',
      tags: ['Work'],
    },
    // Additional placeholder notes...
  ],
});

const searchQuery = computed({
  get: () => state.searchQuery,
  set: (val) => (state.searchQuery = val),
});

const filteredNotes = computed(() => {
  const query = state.searchQuery.toLowerCase();
  return state.notes.filter(
    (n) =>
      n.title.toLowerCase().includes(query) ||
      n.contentSnippet.toLowerCase().includes(query)
  );
});

// Placeholder methods for future implementation
function createNote() {
  // TODO: open modal or navigate to create note view
  console.log('Create note clicked');
}

function editNote(note) {
  // TODO: open modal or navigate to edit note view
  console.log('Edit note', note.id);
}

function deleteNote(noteId) {
  // TODO: implement delete logic
  console.log('Delete note', noteId);
}
</script>

<style scoped>
.main-container {
  width: 100%;
  max-width: 800px;
  display: flex;
  flex-direction: column;
  position: relative;
  background-color: #FFFFFF; /* Secondary */
  padding: 16px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
  border-radius: 8px;
}

/* Search Bar */
.search-bar {
  margin-bottom: 16px;
}
.search-bar input {
  width: 100%;
  padding: 8px 12px;
  border: 1px solid #ddd;
  border-radius: 4px;
}

/* Notes List */
.notes-list {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(240px, 1fr));
  grid-gap: 16px;
}
.note-card {
  background-color: #FFFFFF; /* Secondary */
  border: 1px solid #eee;
  border-radius: 6px;
  padding: 12px;
  cursor: pointer;
  transition: box-shadow 0.2s ease;
}
.note-card:hover {
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
}
.note-title {
  margin: 0 0 8px 0;
  color: #4A90E2; /* Primary */
}
.note-snippet {
  margin: 0 0 12px 0;
  color: #555;
  font-size: 0.9em;
}
.tags {
  display: flex;
  flex-wrap: wrap;
  gap: 4px;
}
.tag-label {
  background-color: #F5A623; /* Accent */
  color: #FFFFFF;
  padding: 2px 6px;
  border-radius: 4px;
  font-size: 0.75em;
}

/* Floating Action Button */
.fab {
  position: fixed;
  bottom: 24px;
  right: 24px;
  width: 56px;
  height: 56px;
  border: none;
  border-radius: 50%;
  background-color: #4A90E2; /* Primary */
  color: #FFFFFF;
  font-size: 2em;
  line-height: 0;
  cursor: pointer;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.2);
  display: flex;
  align-items: center;
  justify-content: center;
}
.fab:hover {
  background-color: #417dcc;
}
</style>
