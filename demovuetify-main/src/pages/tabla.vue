

<template>
    <v-card
      flat
      title="Tabla Incoherente"
    >
      <template v-slot:text>
        <v-text-field
          v-model="search"
          label="Buscar"
          prepend-inner-icon="mdi-magnify"
          single-line
          variant="outlined"
          hide-details
        ></v-text-field>
      </template>
  
      <v-data-table
        :headers="headers"
        :items="desserts"
        :search="search"
      ></v-data-table>
    </v-card>
  </template>

<script setup>
import { ref, onMounted } from 'vue';

const search = ref('');
const headers = ref([
  { align: 'start', key: 'name', sortable: false, title: 'Nombre' },
  { key: 'calories', title: 'Si' },
  { key: 'fat', title: 'Grasa' },
  { key: 'carbs', title: 'Booleano' },
  { key: 'protein', title: 'Proteina (g)' },
  { key: 'iron', title: 'Hierro (%)' },
]);

const desserts = ref([]);

onMounted(async () => {
  try {
    const response = await fetch('https://jsonplaceholder.typicode.com/todos');
    const data = await response.json();
    desserts.value = data.map((item) => ({
      name: item.title,
      calories: item.userId,
      fat: item.id,
      carbs: item.completed,
      protein: 0, // Set your desired value
      iron: 0, // Set your desired value
    }));
  } catch (error) {
    console.error('Error fetching data:', error);
  }
});
</script>
