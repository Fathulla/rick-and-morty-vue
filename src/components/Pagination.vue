<template>
  <div v-if="info" class="pagination_wrapper">
    <button @click="changePage(info.prev)" :disabled="!info.prev">
      Предыдущая
    </button>
    <span v-if="info.pages"
      >Страница {{ info.current }} из {{ info.pages }}</span
    >
    <button @click="changePage(info.next)" :disabled="!info.next">
      Следующая
    </button>
  </div>
</template>

<script>
export default {
  name: "Pagination",
  props: {
    info: {
      type: Object,
      required: true,
    },
  },
  emits: ["changePage"],
  setup(props, { emit }) {
    const changePage = (url) => {
      if (url) {
        const urlParams = new URLSearchParams(new URL(url).search);
        const page = urlParams.get("page");
        emit("changePage", page);
      }
    };

    return {
      changePage,
    };
  },
};
</script>
