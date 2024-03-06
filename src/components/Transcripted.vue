<template>
  <div>
    <p><strong>Fichier : </strong>{{ transcription.file_name }}</p>
    <p><strong>Transcription : </strong>{{ transcription.transcription }}</p>
  </div>
</template>

<script setup>
import { defineProps } from 'vue';

const props = defineProps({
  transcription: {
    type: Object,
    required: true
  }
});
</script>
