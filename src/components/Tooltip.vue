<template>
  <div class="tooltip-text">
    {{ text }}
  </div>
</template>
<script>
export default {
  name: "Tooltip",
  props: {
    text: {
      type: String,
      required: true,
    },
  },
};
</script>
<style scoped>
.tooltip-text {
  position: absolute;
  width: 120px;
  left: 70px;
  background-color: rgb(224, 224, 224);
  color: #000;
  text-align: center;
  border-radius: 6px;
  padding: 5px 0;
  z-index: 1;
  font-size: 15px;
  font-weight: bold;
}

.tooltip-text::after {
  content: "";
  position: absolute;
  top: 50%;
  right: 100%;
  margin-top: -5px;
  border-width: 5px;
  border-style: solid;
  border-color: transparent rgb(224, 224, 224) transparent transparent;
}
</style>
