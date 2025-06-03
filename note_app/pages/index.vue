<template>
  <div class="page-container">
    <MainContainer />
  </div>
</template>

<script setup>
// PUBLIC_INTERFACE
// This page serves as the entry point for the NoteEase app and renders the main container.
import MainContainer from '~/components/MainContainer.vue';
</script>

<style scoped>
.page-container {
  display: flex;
  justify-content: center;
  padding: 16px;
  background-color: #FFFFFF; /* Secondary color */
}
</style>
