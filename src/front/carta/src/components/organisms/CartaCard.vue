<template>
  <div class="block w-32 h-40 bg-blue-200">
    <img :src="imgPath" :alt="this.char"/>
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
      return process.env.BASE_URL + `assets/cards/${this.char}.png`;
    },
  },
};
</script>
