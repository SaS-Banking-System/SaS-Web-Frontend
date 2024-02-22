<script setup>
const props = defineProps(["rotation", "color"]);
</script>

<template>
  <svg
    :style="{ rotate: `${props.rotation}deg`, color: props.color }"
    xmlns="http://www.w3.org/2000/svg"
    fill="none"
    viewBox="0 0 24 24"
    stroke-width="1.5"
    stroke="currentColor"
    class="w-6 h-6"
  >
    <path
      stroke-linecap="round"
      stroke-linejoin="round"
      d="M12 4.5v15m7.5-7.5h-15"
    />
  </svg>
</template>

<style scoped>
svg {
  width: 2.4rem;
}
</style>
