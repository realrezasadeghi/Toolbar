<template>
  <Toolbar @select-mode="selectMode" />
  <div class="text-center p-2">
    <span class="text-select-mode">Chosen Mode : {{ text }}</span>
  </div>
</template>

<script>
import { ref } from "vue";
import Toolbar from "./components/Toolbar.vue";
export default {
  name: "App",
  components: {
    Toolbar,
  },
  setup() {
    const text = ref("Hand");
    const selectMode = (value) => {
      text.value = value;
    };
    return { text, selectMode };
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
.text-select-mode {
  font-weight: bold;
}
</style>
