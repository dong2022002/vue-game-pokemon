<template>
  <div class="scre">
    <h1>InteractScreen Here</h1>
    <card-memmory
      v-for="(card, index) in cardsContext"
      :key="index"
      :imgBackFaceUrl="`images/${card}.png`"
    />
  </div>
</template>

<script>
import CardFlip from "./CardFlip.vue";
export default {
  props: {
    cardsContext: {
      type: Array,
      default: () => [],
    },
  },

  components: {
    CardMemmory: CardFlip,
  },
};
</script>
