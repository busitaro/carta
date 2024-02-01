<template>
  <div class="block w-32 h-40 bg-blue-200">
    <img :src="imgPath" />
  </div>
</template>

<script>
export default {
  props: {
    char: {
      type: String,
      required: true,
    },
  },
  computed: {
    imgPath() {
      console.log(`~/assets/cards/${this.char}.png`);
      return `~/assets/cards/${this.char}.png`;
    },
  },
};
</script>
