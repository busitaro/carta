<template>
  <div class="block w-11/12 h-screen mx-auto bg-blue-100 p-10 flex flex-row">
    <CartaCard
      v-for="(char, index) in charactors"
      :key="index"
      :char="char"
      class="m-2"
    />
    <slot></slot>
  </div>
</template>

<script>
import charactorJson from "~/assets/charactors.json";
import CartaCard from "~/components/organisms/CartaCard.vue";

export default {
  components: {
    CartaCard,
  },
  data() {
    return {
      foo: charactorJson,
      charactors: [],
    };
  },
  mounted() {
    this.charactors = this.getAllCharactors();
  },
  methods: {
    getAllCharactors() {
      const charactors = charactorJson.charactors
      return charactors
    },
  },
};
</script>
