<template>
  <div :class="className">
    <div class="card bg-light">
      <div class="card-body">
        <div>
          <slot v-if="!imgPath" />
        </div>
        <img
          v-if="imgPath"
          :src="imgPath"
          alt=""
          style="object-fit: cover"
          :style="{ width: imgWidth, height: imgHeight}"
        />
        <div class="px-7 py-4">
          <h4 class="card-title">{{ title }}</h4>
          <p class="card-text" :class="{ 'text-truncate': isTrancate }">{{ description }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "LayoutVerticalMenu",
  props: {
    className: {
      type: String,
      default: "col-md-4",
    },
    title: {
      type: String,
      default: "",
    },
    description: {
      type: String,
      default: "",
    },
    imgPath: {
      default: require("~/assets/img/P_20200302_035129.jpg"),
    },
    imgWidth: {
      type: String,
      default: "300px"
    },
    imgHeight: {
      type: String,
      default: "300px"
    },
    isTrancate: {
      type: Boolean,
      default: false
    }
  },
};
</script>