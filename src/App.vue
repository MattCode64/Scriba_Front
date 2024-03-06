<template>
  <nav class="navbar bg-body-tertiary">
    <div class="container-fluid">
      <span class="navbar-brand mb-0 h1">SCRIBA</span>
    </div>
  </nav>

  <div class="container">
    <div class="row">
      <div class="col-12">
        <h1 class="text-center">Scriba</h1>
      </div>
    </div>
  </div>

  <div class="mb-3 text-center">
    <label for="formFile" class="form-label">Upload File</label>
    <div>
      <input class="form-floating" type="file" id="formFile" @change="submitFile">
      <div>
        <Transcripted v-if="transcription" :transcription="transcription" />
      </div>
    </div>
  </div>


</template>


<script setup>
import { ref } from 'vue';
import Transcripted from './components/Transcripted.vue';
import axios from 'axios';

const transcription = ref(null);

async function submitFile(event) {
  const file = event.target.files[0];
  if (!file) return;

  const formData = new FormData();
  formData.append('file', file);

  try {
    const response = await axios.post('http://localhost:8000/transcribe/', formData, {
      headers: {
        'Content-Type': 'multipart/form-data',
      },
    });
    transcription.value = response.data.results[0]; // Assumant que `results` est un tableau
  } catch (error) {
    console.error(error);
  }
}
</script>

<!--<script setup>-->
<!--import HelloWorld from './components/HelloWorld.vue'-->
<!--import TheWelcome from './components/TheWelcome.vue'-->
<!--</script>-->

<!--<template>-->
<!--  <header>-->
<!--    <img alt="Vue logo" class="logo" src="./assets/logo.svg" width="125" height="125" />-->

<!--    <div class="wrapper">-->
<!--      <HelloWorld msg="You did it!" />-->
<!--    </div>-->
<!--  </header>-->

<!--  <main>-->
<!--    <TheWelcome />-->
<!--  </main>-->
<!--</template>-->

<!--<style scoped>-->
<!--header {-->
<!--  line-height: 1.5;-->
<!--}-->

<!--.logo {-->
<!--  display: block;-->
<!--  margin: 0 auto 2rem;-->
<!--}-->

<!--@media (min-width: 1024px) {-->
<!--  header {-->
<!--    display: flex;-->
<!--    place-items: center;-->
<!--    padding-right: calc(var(&#45;&#45;section-gap) / 2);-->
<!--  }-->

<!--  .logo {-->
<!--    margin: 0 2rem 0 0;-->
<!--  }-->

<!--  header .wrapper {-->
<!--    display: flex;-->
<!--    place-items: flex-start;-->
<!--    flex-wrap: wrap;-->
<!--  }-->
<!--}-->
<!--</style>-->