<template>
  <div class="block w-32 h-36">
    <img :src="imgPath" :alt="this.char" :class="{ hidden: !modelValue }" />
  </div>
</template>

<script>
export default {
  props: {
    modelValue: {
      type: Boolean,
    },
    char: {
      type: String,
      required: true,
    },
  },
  computed: {
    imgPath() {
      return process.env.BASE_URL + `assets/cards/${this.char}.png`;
    },
  },
};
</script>
<style scoped>
.hidden {
  visibility: hidden;
}
</style>
