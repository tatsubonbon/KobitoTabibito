<template>
  <div class="row border bg-light rounded px-4 py-2">
      <div class="col-md-4">{{ time | formatDate }}</div>
      <div class="col-md-8">{{ title }}</div>
  </div>
</template>

<script>
export default {
  name: "",
  props: {
    time: {
      type: String,
    },
    title: {
      type: String,
    },
  },
};
</script>
