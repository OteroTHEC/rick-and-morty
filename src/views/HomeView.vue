<script setup>
import { onMounted, ref } from 'vue';
import ListCharacters from '../components/ListCharacters.vue';

const characters = ref([]);

onMounted(async () => {
  try {
    const response = await fetch("https://rickandmortyapi.com/api/character");
    const data = await response.json();
    characters.value = data.results;
  } catch (error) {
    console.error("Erro ao carregr personagens:", error);
  }
});
</script>

<template>
  <main>
    <div class="container">
      <div class="row mt-4">
        <div class="col-sm-12 col-md-12">
          <div class="card">
            <div class="card-body row">
              <ListCharacters 
                v-for="character in characters.value"
                :key="character.id"
                :character="character"
              />
            </div>
          </div>
        </div>
      </div>
    </div>
  </main>
</template>

<style>

</style>

