<template>
  <div class="cards_wrapper">
    <div
      v-for="character in characters"
      :key="character.id"
      class="character-card"
    >
      <img :src="character.image" :alt="character.name" />
      <h2><b>Name:</b> {{ character.name }}</h2>
      <p><b>Status:</b> {{ character.status }}</p>
      <p><b>Species:</b> {{ character.species }}</p>
      <p><b>Gender:</b> {{ character.gender }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "CharacterList",
  props: {
    characters: {
      type: Array,
      required: true,
    },
  },
};
</script>
