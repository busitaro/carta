<template>
  <div class="block w-11/12 h-screen mx-auto bg-blue-100 p-10 flex flex-row">
    <CartaCard
      v-for="(char, index) in charactors"
      v-model="char.visibility"
      :key="index"
      :char="char.char"
      class="m-2"
      @click="judge(char)"
    />
    <slot></slot>
  </div>
</template>

<script>
import CartaCard from "~/components/organisms/CartaCard.vue";

export default {
  components: {
    CartaCard,
  },
  props: {
    allCharactors: {
      type: Array,
      required: true,
    },
  },
  data() {
    return {
      charactors: [],
      visibleTest: true,
    };
  },
  mounted() {
    this.charactors = this.getAllCharactors();
  },
  methods: {
    getAllCharactors() {
      console.log("🐈");
      console.log(this.allCharactors);
      const charactors = this.allCharactors.charactors.map((value) => {
        return {
          char: value,
          visibility: true,
        };
      });
      return charactors;
    },
    judge(char) {
      this.hiddenCard(char);
    },
    hiddenCard(targetChar) {
      const target = this.charactors.find((char) => char == targetChar);
      if (target) {
        target.visibility = false;
      }
    },
  },
};
</script>
