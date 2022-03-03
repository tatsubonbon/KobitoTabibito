<template>
  <div class="card" style="border: none">
    <img
      class="card-img"
      style="object-fit: cover"
      :style="'height:' + height +'vh'"
      :src="imgPath"
      alt=""
    />
    <div class="card-img-overlay">
      <div class="text-center">
        <h1 :class="color">{{ title }}</h1>
        <p v-if="message" :class="color">{{ message }}</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "LayoutVisual",
  props: {
    color: {
      type: String,
      default: "text-shadow"
    },
    title: {
      type: String,
      default: "",
    },
    message: {
      type: String,
      default: "",
    },
    visual: {
      type: String,
      default: "visual-home",
    },
    height: {
      type: Number,
      default: 75,
    },
    imgPath: {
    },
  },
};
</script>