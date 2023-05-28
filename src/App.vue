<script setup>
import { ref, computed } from "vue";
//Data
let counter = ref(0)
let favorites = ref([])

//Methods
const increase = () => {
  counter.value++
}

const decrease = () => {
  counter.value--
}

const addToFavorites = () => {
  favorites.value.push(counter.value)
}

const removeToFavorites = () => {
  let index = favorites.value.findIndex((favorite) => counter.value == favorite)
  favorites.value.splice(index, 1)
}


//Computed
const className = computed(() => {
  if (counter.value > 0) {
    return 'positive'
    
  }else if(counter.value < 0) {
    return 'negative'
  }else {
    return 'zero'
  }
})

const hasFavorite = computed(() => {
  return favorites.value.some(favorite => counter.value == favorite)
})


</script>

<template lang="">
  <div class="container text-center mt-3">
    <h2 :class="className">Valor: {{ counter }}</h2>
    <div class="btn-group">
      <button @click="increase()" class="btn btn-success">Aumentar</button>
      <button @click="decrease()" class="btn btn-danger">Disminuir</button>
      <button @click="addToFavorites()" :disabled="hasFavorite" class="btn btn-primary">Añadir a Favoritos</button>
      <button @click="removeToFavorites()" :disabled="!hasFavorite" class="btn btn-warning">Remover a Favoritos</button>
    </div>
  </div>
  <div class="container text-center mt-3">
    <h2>Números Favoritos</h2>
    <div class=" d-flex aling-items-center justify-content-center">
      <table class="table table-bordered" style="width: 200px">
        <thead>
          <tr>
            <th scope="col">Número</th>
          </tr>
        </thead>
        <tbody>
          <tr v-if="!favorites.length">
            <span>No tiene Números favoritos...</span>
          </tr>
          <tr v-for="favorite in favorites">
            <th scope="row">{{ favorite }}</th>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<style>
  .negative {
    color: red;
  }

  .positive {
    color: green;
  }

  .zero {
    color: black;
  }
</style>