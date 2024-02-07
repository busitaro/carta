<template>
  <div class="block w-11/12 h-screen mx-auto bg-blue-100 p-10 flex flex-row">
    <CartaCard
      v-for="(char, index) in charactors"
      v-model="char.visibility"
      :key="index"
      :char="char.char"
      class="m-2"
      @click="judge(char.char)"
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
    gameCount: {
      type: Number,
      required: true,
    },
    allCharactors: {
      type: Array,
      required: true,
    },
    nowCharactor: {
      type: String,
    },
  },
  data() {
    return {
      charactors: [],
      visibleTest: true,
    };
  },
  watch: {
    gameCount(value) {
      console.log(`gameCountが変わりました: ${value}`);
      // ゲーム開始
      this.startGame();
    },
  },
  methods: {
    startGame() {
      this.charactors = this.setUpAllCharactors(this.allCharactors);
    },
    setUpAllCharactors(allCharactors) {
      const charactors = allCharactors.map((value) => {
        return {
          char: value,
          visibility: true,
        };
      });
      return charactors;
    },
    judge(char) {
      console.log(`現在の文字「${this.nowCharactor}」`);
      console.log(`選んだ文字「${char}」`);
      if (char === this.nowCharactor) {
        this.correct(char);
      } else {
        this.incorrect(char);
      }
    },
    correct(char) {
      console.log(`🌸 正解！！！`);
      this.$emit("correct");
      this.hiddenCard(char);
    },
    incorrect() {
      console.log(`🐣 不正解！！！`);
    },
    hiddenCard(targetChar) {
      console.log(this.charactors);
      const target = this.charactors.find((char) => char.char === targetChar);
      if (target) {
        target.visibility = false;
      }
    },
  },
};
</script>
