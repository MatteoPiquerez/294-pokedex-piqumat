<template>
  <v-container>
    <h1 class="text-h3 text-center my-6">Pokédex</h1>

    <!-- Squelettes de chargement pendant la requête API -->
    <v-row v-if="pokemonStore.isLoading">
      <v-col
        v-for="n in 8"
        :key="n"
        cols="12"
        sm="6"
        md="4"
        lg="3"
      >
        <v-skeleton-loader
          type="image, article"
          height="350"
        />
      </v-col>
    </v-row>

    <!-- Message d'erreur si aucun Pokémon chargé -->
    <v-alert
      v-else-if="pokemonStore.pokemons.length === 0"
      type="error"
      variant="tonal"
      class="mb-6"
    >
      Impossible de charger les Pokémon. Vérifiez que l'API tourne sur
      {{ apiUrl }}.
    </v-alert>

    <!-- Grille de cartes (cas normal) -->
    <v-row v-else>
      <!-- ... vos v-col + PokemonCard ... -->
    </v-row>
    <v-row>
      <v-col
        v-for="pokemon in pokemons"
        :key="pokemon.id"
        cols="12"
        sm="6"
        md="4"
        lg="3"
      >
        <pokemon-card :pokemon="pokemon" />
      </v-col>
    </v-row>
  </v-container>
</template>

<script setup>
// Import du store et de storeToRefs
import { usePokemonStore } from '@/stores/pokemonStore'
import { storeToRefs } from 'pinia'
import PokemonCard from '@/components/PokemonCard.vue'

// URL de l'API pour le message d'erreur
const apiUrl = import.meta.env.VITE_API_URL || 'http://localhost:3535'

// Instancier le store
const pokemonStore = usePokemonStore()

// Destructurer le state en gardant la réactivité
// storeToRefs convertit chaque propriété du state en ref
const { pokemons } = storeToRefs(pokemonStore)
</script>
