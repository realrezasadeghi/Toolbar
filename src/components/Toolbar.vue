<template>
  <div class="toolbar">
    <div class="col position-relative">
      <div
        v-for="(item, index) in toolSet"
        :key="index"
        class="d-flex justify-content-center align-items-center position-relative p-2"
        :class="{ 'border border-dark': index == 0 }"
      >
        <i
          :class="[
            'tool',
            'bi',
            item.icon,
            { active: indexToolActive == index },
          ]"
          @click="selectTool(index, item.name)"
          @mouseover="showTooltip(index)"
          @mouseout="hideTooltip()"
        ></i>
        <!-- tooltip for every tool -->
        <tooltip :text="item.name" v-show="indexToolHover == index" />
      </div>
    </div>
  </div>
</template>

<script>
import { ref, onMounted } from "vue";
import Tooltip from "./Tooltip.vue";

export default {
  components: { Tooltip },
  name: "Toolbar",
  emits: ["select-mode"],
  setup(props, { emit }) {
    // tool hover
    const indexToolHover = ref(null);
    // tool active
    const indexToolActive = ref(0);
    const toolSet = ref([
      { name: "Hand", icon: "bi-hand-index-thumb", shortKey: "Escape" },
      { name: "Crop", icon: "bi-crop", shortKey: "1" },
      { name: "Pencil", icon: "bi-pencil-fill", shortKey: "2" },
      { name: "Magic", icon: "bi-magic", shortKey: "3" },
      { name: "Brush", icon: "bi-brush-fill", shortKey: "4" },
      { name: "Eraser", icon: "bi-eraser-fill", shortKey: "5" },
      { name: "Map", icon: "bi-geo-alt-fill", shortKey: "6" },
      { name: "Target", icon: "bi-bullseye", shortKey: "7" },
    ]);
    const showTooltip = (index) => {
      indexToolHover.value = index;
    };
    const hideTooltip = () => {
      indexToolHover.value = null;
    };
    const selectTool = (index, name) => {
      indexToolActive.value = index;
      emit("select-mode", name);
    };
    onMounted(() => {
      document.addEventListener("keydown", (ev) => {
        const key = ev.key;
        const tool = toolSet.value.find((item) => item.shortKey === key);

        if (key > 0 && key < 8) {
          indexToolActive.value = key;
          emit("select-mode", tool.name);
        } else if (key === "Escape") {
          indexToolActive.value = 0;
          emit("select-mode", tool.name);
        }
      });
    });
    return {
      toolSet,
      indexToolHover,
      indexToolActive,
      showTooltip,
      hideTooltip,
      selectTool,
    };
  },
};
</script>

<style scoped>
.toolbar {
  background-color: rgb(25, 25, 43);
  position: fixed;
  height: 100%;
  width: 65px;
  left: 0;
}

.tool {
  cursor: pointer;
  font-size: 23px;
  transition: 0.2s ease-in;
}
.tool:hover {
  color: white;
  transform: scale(1.3);
}
.active {
  transition: 0.2 ease-in;
  color: green;
  transform: scale(1.3);
}
</style>
