<template>
  <h2 class="py-2">
      <slot />
  </h2>
</template>

<script>
export default {
    name: 'BaseHeading',
}
</script>

<style scoped>
h2 {
    font-size: 30px;
    font-weight: bold;
}
</style>