<template>
  <div class="container mt-5">
    <h1>Calculatrice</h1>

    <!-- Sélection de l'opération -->
    <form action="" @submit.prevent="validation">
      <div class="form-check mb-3">
        <div class="form-group">
          <input
            class="form-check-input"
            type="radio"
            v-model="op"
            value="add"
            id="add"
          />
          <label class="form-check-label" for="add">Addition</label>
        </div>
        <div class="form-group">
          <input
            class="form-check-input"
            type="radio"
            v-model="op"
            value="sous"
            id="sous"
          />
          <label class="form-check-label" for="sous">Soustraction</label>
        </div>
        <div class="form-group">
          <input
            class="form-check-input"
            type="radio"
            v-model="op"
            value="mult"
            id="mult"
          />
          <label class="form-check-label" for="mult">Multiplication</label>
        </div>
        <div class="form-group">
          <input
            class="form-check-input"
            type="radio"
            v-model="op"
            value="div"
            id="div"
          />
          <label class="form-check-label" for="div">Division</label>
        </div>
      </div>
    </form>

    <!-- Formulaire pour entrer les valeurs -->
    <form action="" @submit.prevent="validation" v-if="op">
      <div class="mb-3">
        <label for="val1" class="form-label">Premier nombre</label>
        <input
          type="number"
          class="form-control"
          id="val1"
          v-model.number="val1"
          placeholder="Valeur 1"
        />
      </div>
      <div class="mb-3">
        <label for="val2" class="form-label">Deuxième nombre</label>
        <input
          type="number"
          class="form-control"
          id="val2"
          v-model.number="val2"
          placeholder="Valeur 2"
        />
      </div>
      <div class="mb-3">
        <button type="submit" class="btn btn-primary">Calculer</button>
      </div>
    </form>

    <!-- Affichage du résultat ou du message d'erreur -->
    <div v-if="result !== null" class="alert alert-success">
      Résultat : {{ result }}
    </div>
    <div v-if="errorMessage" class="alert alert-danger">
      {{ errorMessage }}
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const op = ref('');
const val1 = ref(); 
const val2 = ref(); 
const result = ref(null); 
const errorMessage = ref(''); 


function validation() {
  errorMessage.value = ''; 
  result.value = null; 

  switch (op.value) {
    case 'add':
      result.value = val1.value + val2.value;
      break;
    case 'sous':
      result.value = val1.value - val2.value;
      break;
    case 'mult':
      result.value = val1.value * val2.value;
      break;
    case 'div':
      if (val2.value === 0) {
        errorMessage.value = 'La division par zéro est impossible.';
      } else {
        result.value = val1.value / val2.value;
      }
      break;
    default:
      errorMessage.value = 'Opération inconnue.';
  }
  val1.value = 0;
  val2.value = 0;

}
</script>

<style scoped>
.container {
  max-width: 500px;
  margin-top: 50px;
}
</style>
