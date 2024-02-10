<template>
  <div class="block w-32 h-36">
    <img v-if="modelValue" :src="imgPath" :alt="this.char" />
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
