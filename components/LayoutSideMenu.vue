<template>
  <div class="pb-2">
    <div class="bg-light px-4 py-4">
      <div class="row">
        <div v-if="!imgPath" class="col-md-6">
          <slot />
        </div>
        <img v-if="imgPath" :src="imgPath" alt="" class="col-md-6" />
        <div class="col-md-6">
          <h4>{{ title }}</h4>
          <p>{{ description }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
    name: "LayoutSideMenu",
    props: {
        title: {
            type: String,
            default: ''
        },
        description: {
            type: String,
            default: ''
        },
        imgPath: {
        }
    }
};
</script>
