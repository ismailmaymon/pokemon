<script>
import PokemonModal from "../components/PokemonModal.vue";
import PokemonJson from "../json/pokemon.json";

export default {
  components: {
    PokemonModal,
  },
  data() {
    return {
      pokemonDetail: {},
      Pokemon: [],
      isModalOpen: false,
      searchQuery: "", // For storing the search input
    };
  },
  mounted() {
    this.Pokemon = PokemonJson;
  },
  computed: {
    filteredPokemon() {
      // Filter Pokémon based on the search query
      return this.Pokemon.filter((item) =>
        item.name.toLowerCase().includes(this.searchQuery.toLowerCase())
      );
    },
  },
  methods: {
    handleIsModalOpen(item) {
      this.pokemonDetail = item;
      this.isModalOpen = true;
    },
  },
};
</script>

<template>
  <div>
    <div class="sm:mx-auto sm:container sm:py-16 py-5 sm:px-5 px-4">
      <h1 class="text-3xl font-medium text-blue-950 text-center">Pokedex</h1>
      <div class="flex justify-center mt-6">
        <input
          type="text"
          v-model="searchQuery"
          class="border rounded-lg px-3 py-2 sm:w-80 w-full focus:outline-none focus:ring-2 focus:ring-blue-500 transition"
          placeholder="Search for a Pokémon"
        />
      </div>
      <div
        v-if="filteredPokemon.length > 0"
        class="mt-6 grid grid-cols-2 gap-2 sm:flex-wrap sm:gap-4 sm:flex sm:justify-center"
      >
        <div
          class="bg-blue-950 shadow cursor-pointer sm:w-60 w-full rounded-lg sm:pt-16 pt-10 pb-6 px-2"
          @click="handleIsModalOpen(item)"
          v-for="item in filteredPokemon"
          :key="item.id"
        >
          <img :src="item.imageUrl" alt="" class="w-20 min-h-32 mx-auto" />
          <div>
            <h2 class="text-center pt-10 text-white">{{ item.name }}</h2>
            <div class="flex justify-center mt-5 gap-2">
              <h2
                class="bg-blue-900 text-white rounded-full px-[12px] shadow py-[2px]"
              >
                {{ item.firstName }}
              </h2>
              <h2
                class="bg-blue-900 text-white rounded-full px-[12px] shadow py-[2px]"
              >
                {{ item.secondName }}
              </h2>
            </div>
          </div>
        </div>
      </div>
      <div v-else>
        <div class="text-center text-gray-500 w-full mt-4">
          <h2>No Pokémon found matching your search.</h2>
        </div>
      </div>
    </div>
    <div>
      <PokemonModal
        :isModalOpen="isModalOpen"
        @closeModal="isModalOpen = false"
        :pokemonDeatil="pokemonDetail"
      />
    </div>
  </div>
</template>
