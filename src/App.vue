<template>
  <div id="app">
    <h1>Персонажи из Рик и Морти</h1>
    <FilterSection @applyFilters="applyFilters" />
    <CharacterList :characters="characters" />
    <Pagination :info="pageInfo" @changePage="changePage" />
  </div>
</template>

<script>
import { ref, onMounted } from "vue";
import axios from "axios";
import FilterSection from "./components/FilterSection.vue";
import CharacterList from "./components/CharacterList.vue";
import Pagination from "./components/Pagination.vue";

export default {
  name: "App",
  components: {
    FilterSection,
    CharacterList,
    Pagination,
  },
  setup() {
    const characters = ref([]);
    const pageInfo = ref({});
    const filters = ref({ name: "", status: "" });

    const fetchCharacters = async (page = 1) => {
      try {
        const response = await axios.get(
          `https://rickandmortyapi.com/api/character`,
          {
            params: {
              page,
              name: filters.value.name,
              status: filters.value.status,
            },
          }
        );
        characters.value = response.data.results;
        pageInfo.value = {
          prev: response.data.info.prev,
          next: response.data.info.next,
          current: page,
          pages: response.data.info.pages,
        };
      } catch (error) {
        console.error(error);
      }
    };

    const applyFilters = (newFilters) => {
      filters.value = newFilters;
      fetchCharacters();
    };

    const changePage = (page) => {
      fetchCharacters(page);
    };

    onMounted(() => {
      fetchCharacters();
    });

    return {
      characters,
      pageInfo,
      applyFilters,
      changePage,
    };
  },
};
</script>
