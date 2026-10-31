<script setup>
import { ref, onMounted } from 'vue'

const pokemon = ref(null)
const loading = ref(false)
const error = ref(null)

async function fetchPokemon() {
  loading.value = true
  error.value = null

  try {
    const randomId = Math.floor(Math.random() * 1025) + 1
    const response = await fetch(`https://pokeapi.co/api/v2/pokemon/${randomId}`)

    if (!response.ok) {
      throw new Error('Failed to fetch Pokemon data')
    }

    const data = await response.json()
    pokemon.value = data

    console.log(pokemon.value)
  } catch (err) {
    error.value = 'Unable to retrieve Pokemon data. Please try again.'
    console.error('Error fetching Pokemon data', err)
  } finally {
    loading.value = false
  }
}

onMounted(() => {
  fetchPokemon()
})

function handleImageError(event) {
  const fallback = pokemon.value.sprites.other['official-artwork'].front_default
    || pokemon.value.sprites.front_default

  if (fallback && event.target.src !== fallback) {
    event.target.src = fallback
  }
}
</script>

<template>
  <main>
    <h1>Pokemon Explorer API</h1>
    <p>
      Discover and explore various Pokemon using the PokeAPI!
    </p>

    <p v-if="loading">Loading Pokemon...</p>
    <p v-if="error">{{ error }}</p>
    <div v-if="pokemon && !loading && !error" class="pokemon-card">
      <h2>{{ pokemon.name }}</h2>

      <img
        :key="pokemon.id"
        :src="`https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/versions/generation-ix/legends-za/${pokemon.id}.webp`"
        :alt="pokemon.name"
        @error="handleImageError"
      />

      <p>Pokedex Number: {{ pokemon.id }}</p>
      <p>Type: {{ pokemon.types.map(type => type.type.name).join(', ') }}</p>
      <p>
        Height: {{ (pokemon.height / 10).toFixed(2) }} m
        ({{ (pokemon.height * 3.93701).toFixed(1) }} in)
      </p>
      <p>
        Weight: {{ (pokemon.weight / 10).toFixed(1) }} kg
        ({{ (pokemon.weight * 0.220462).toFixed(1) }} lbs)
      </p>
    </div>

    <button @click="fetchPokemon" :disabled="loading">Get a Random Pokemon</button>
  </main>
</template>

<style scoped>
main {
  min-height: 100vh;
  background-color: #c62828;
  text-align: center;
  padding: 40px 20px;
  box-sizing: border-box;
  font-family: Arial, sans-serif;
}

h1 {
  color: white;
  font-size: 36px;
  margin-bottom: 10px;
}

main > p {
  color: white;
  margin-bottom: 25px;
}

.pokemon-card {
  background-color: #ffffff;
  border-radius: 15px;
  padding: 25px;
  max-width: 350px;
  margin: 20px auto;
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
}

.pokemon-card h2 {
  text-transform: capitalize;
  font-size: 28px;
  color: #333;
}

.pokemon-card img {
  width: 180px;
  height: 180px;
  object-fit: contain;
}

.pokemon-card p {
  color: #555;
  font-size: 16px;
}

button {
  background-color: white;
  color: #c62828;
  border: none;
  border-radius: 8px;
  padding: 12px 24px;
  font-size: 16px;
  font-weight: bold;
  cursor: pointer;
  margin-top: 15px;
}

button:hover {
  background-color: #f5f5f5;
  transform: scale(1.05);
}

button:disabled {
  background-color: #ccc;
  cursor: not-allowed;
}
</style>
