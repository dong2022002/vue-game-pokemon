<template>
  <main-screen
    v-if="statusMatch === 'default'"
    @onStart="onHandleBeforeStart($event)"
  />
  <interact-screen v-if="statusMatch === 'match'" />
</template>

<script>
import MainScreen from "./components/MainScreen.vue";
import InteractScreen from "./components/InteractScreen.vue";
export default {
  name: "App",
  components: {
    MainScreen,
    InteractScreen,
  },
  data() {
    return {
      statusMatch: "default",
    };
  },
  methods: {
    onHandleBeforeStart(config) {
      console.log("running ,", config);

      this.statusMatch = "match";
    },
  },
};
</script>
