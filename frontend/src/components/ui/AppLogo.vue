<template>
  <svg
    :width="size"
    :height="size"
    viewBox="0 0 28 28"
    class="shrink-0"
    role="img"
    aria-label="Soundkeep"
  >
    <circle cx="14" cy="14" r="14" class="fill-accent" />
    <g class="fill-bg">
      <ellipse cx="9.6" cy="19.2" rx="3" ry="2.3" />
      <ellipse cx="17.4" cy="17.2" rx="3" ry="2.3" />
      <polygon points="11.2,8.6 20.6,6.4 20.6,9 11.2,11.2" />
      <rect x="11.2" y="8.6" width="1.8" height="10.4" />
      <rect x="18.8" y="6.8" width="1.8" height="10.2" />
    </g>
  </svg>
</template>

<script setup>
defineProps({ size: { type: Number, default: 28 } })
</script>
