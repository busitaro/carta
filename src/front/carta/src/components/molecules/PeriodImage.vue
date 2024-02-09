<template>
  <div class="p-fixed" v-if="modelValue">
    <img :src="imgPath" alt="correct" />
  </div>
</template>

<script>
export default {
  props: {
    modelValue: {
      type: Boolean,
    },
  },
  computed: {
    imgPath() {
      return process.env.BASE_URL + `assets/images/correct1.png`;
    },
  },
};
</script>
<style scoped>
.p-fixed {
  position: fixed;
  top: 0;
  left: 0;
  background: #000;
}
.p-fixed img {
  position: fixed;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  max-width: 100%;
  max-height: 100%;
  margin: auto;
}
</style>
