<template>
  <div class="filters_wrapper">
    <input v-model="name" placeholder="Имя" />
    <select v-model="status">
      <option value="">Все</option>
      <option value="alive">Живой</option>
      <option value="dead">Мертвый</option>
      <option value="unknown">Неизвестно</option>
    </select>
    <button @click="applyFilters">Применить</button>
  </div>
</template>

<script>
import { ref } from "vue";

export default {
  name: "FilterSection",
  emits: ["applyFilters"],
  setup(_, { emit }) {
    const name = ref("");
    const status = ref("");

    const applyFilters = () => {
      emit("applyFilters", { name: name.value, status: status.value });
    };

    return {
      name,
      status,
      applyFilters,
    };
  },
};
</script>
