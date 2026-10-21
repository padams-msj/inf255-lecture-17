<script setup>
import { ref, computed } from "vue";
import AppHeader from "./components/AppHeader.vue";
import AnimalCard from "./components/AnimalCard.vue";

const animals = ref([
  { id: 1, name: "Biscuit", species: "Dog", age: 3, adopted: false },
  { id: 2, name: "Pickles", species: "Cat", age: 5, adopted: true },
  { id: 3, name: "Waffles", species: "Rabbit", age: 1, adopted: false },
  { id: 4, name: "Noodle", species: "Dog", age: 2, adopted: false },
  { id: 5, name: "Mochi", species: "Cat", age: 7, adopted: false },
  { id: 6, name: "Pepper", species: "Guinea pig", age: 2, adopted: true },
]);

const adoptedCount = computed(() => {
  const adoptedAnimals = animals.value.filter(function (animal) {
    return animal.adopted;
  });
  return adoptedAnimals.length;
});

function toggleAdopted(animal) {
  animal.adopted = !animal.adopted;
}
</script>

<template>
  <AppHeader :total="animals.length" :adopted="adoptedCount" />

  <div class="grid">
    <AnimalCard
      v-for="animal in animals"
      :key="animal.id"
      :animal-data="animal"
      @toggle="toggleAdopted(animal)"
    />
  </div>
</template>

<style scoped>
.grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
  gap: 1rem;
}
</style>
