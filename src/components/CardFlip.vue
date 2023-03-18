<template>
  <div
    class="card"
    :class="{ disabled: isDisabled }"
    :style="{
      height: `${(800 - 16 * 4) / Math.sqrt(cardsContext.length) - 16}px`,
      width: `${
        (((800 - 16 * 4) / Math.sqrt(cardsContext.length) - 16) * 3) / 4
      }px`,
      perspective: `${
        ((((800 - 16 * 4) / Math.sqrt(cardsContext.length) - 16) * 3) / 4) * 2
      }px`,
    }"
  >
    <div
      class="card__inner"
      :class="{ 'is-flipped': isFlipped }"
      @click="onToggleFlipCard"
    >
      <div class="card__face card__face--font">
        <div
          class="card__content"
          :style="{
            backgroundSize: `${
              (((800 - 16 * 4) / Math.sqrt(cardsContext.length) - 16) * 3) /
              4 /
              3
            }px ${
              (((800 - 16 * 4) / Math.sqrt(cardsContext.length) - 16) * 3) /
              4 /
              3
            }px`,
          }"
        ></div>
      </div>
      <div class="card__face card__face--back">
        <div
          class="card__content"
          :style="{
            backgroundImage: `url(${require('@/assets/' + imgBackFaceUrl)})`,
          }"
        ></div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    card: {
      type: [String, Number, Array, Object],
    },
    imgBackFaceUrl: {
      type: String,
      require: true,
    },
    cardsContext: {
      type: Array,
      default: function () {
        return [];
      },
    },
  },
  methods: {
    onFlipBackCard() {
      this.isFlipped = false;
    },
    onToggleFlipCard() {
      if (this.isDisabled) return false;
      this.isFlipped = !this.isFlipped;
      if (this.isFlipped) this.$emit("onFlip", this.card);
    },
    onSetDisableMode() {
      this.isDisabled = true;
    },
  },
  data() {
    return {
      isDisabled: false,
      isFlipped: false,
    };
  },
};
</script>

<style lang="css" scoped>
.card__face--font .card__content {
  background: url("../assets/images/icon_back.png") no-repeat center;
  height: 100%;
  width: 100%;
}
.card__face--back .card__content {
  background-size: contain;
  background-position: center center;
  background-repeat: no-repeat;
  height: 100%;
  width: 100%;
}
.card {
  display: inline-block;
  margin: 0.5rem;
}
.card.disabled .card__inner {
  cursor: default;
}
.card__inner {
  width: 100%;
  height: 100%;
  transition: transform 0.5s;
  transform-style: preserve-3d;
  cursor: pointer;
  position: relative;
}
.card__inner.is-flipped {
  transform: rotateY(-180deg);
}

.card__face {
  position: absolute;
  width: 100%;
  height: 100%;
  backface-visibility: hidden;
  overflow: hidden;
  border-radius: 1rem;
  padding: 1rem;
  box-shadow: 0 3px 10px 3px rgba(0, 0, 0, 0.3);
}

.card__face--back {
  background-color: var(--light);
  transform: rotateY(-180deg);
}
</style>
