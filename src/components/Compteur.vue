<template>
  <div>
    <h1>Compteur interactif</h1><br/>
  
    <button @click="decremente" :disabled="compteur === 0">-</button>
    <button @click="incrementer" :disabled="compteur === 10">+</button><br />
  
    <h2>Compteur : {{ compteur }}</h2><br />
    
    <h2>Historique des actions</h2>
    <button @click="toggleHistorique">
      {{ afficherHistorique ? 'Masquer' : 'Afficher' }} l'historique
    </button>
    <ul v-if="afficherHistorique">
      <li
        v-for="(element, index) in liste"
        :key="index"
        :class="index % 2 === 0 ? 'even' : 'odd'"
      >
        {{ element }}
      </li>
    </ul>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const liste = ref([]);
const compteur = ref(0);
const afficherHistorique = ref(true);

const incrementer = () => {
  compteur.value++;
  liste.value.unshift(new Date().toLocaleString() + " - Incrémentation (+)");
};

const decremente = () => {
  compteur.value--;
  liste.value.unshift(new Date().toLocaleString() + " - Décrémentation (-)");
};

const toggleHistorique = () => {
  afficherHistorique.value = !afficherHistorique.value;
};
</script>

<style>
.even {
  background-color: #f0f0f0;
  color: green;
}

.odd {
  background-color: #dfefff;
  color: red;
}

button {
  margin: 5px;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  padding: 5px;
  border-bottom: 1px solid #ccc;
}
</style>
