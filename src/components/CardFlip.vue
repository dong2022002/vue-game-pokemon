<template>
  <div class="card">
    <div
      class="card__inner"
      :class="{ 'is-flipped': isFlipped }"
      @click="onToggleFlipCard"
    >
      <div class="card__face card__face--font">
        <div class="card__content"></div>
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
import { stringLiteral } from "@babel/types";

export default {
  props: {
    imgBackFaceUrl: {
      type: stringLiteral,
      require: true,
    },
  },
  data() {
    return {
      isFlipped: false,
    };
  },
  methods: {
    onToggleFlipCard() {
      console.log("123");
      this.isFlipped = !this.isFlipped;
    },
  },
};
</script>

<style lang="css" scoped>
.card__face--font .card__content {
  background: url("../assets/images/icon_back.png") no-repeat center;
  background-size: 40px 40px;
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
  width: 90px;
  height: 120px;
  display: inline-block;
  margin: 0.5rem;
}
.card__inner {
  width: 100%;
  height: 100%;
  transition: transform 1s;
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
