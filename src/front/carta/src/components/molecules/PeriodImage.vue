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
      required: true,
    },
    imgPath: {
      type: String,
      required: true,
    }
  },
  watch: {
    async modelValue(value) {
      const sleep = msec => new Promise(resolve => setTimeout(resolve, msec));
      if (value) {
        await sleep(1000)
        this.$emit('update:modelValue', false)
      }
    }
  }
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
