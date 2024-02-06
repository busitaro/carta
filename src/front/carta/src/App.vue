<template>
  <CartaTable :all-charactors="allCharactors"> </CartaTable>
</template>

<script>
import charactorJson from "~/assets/charactors.json";
import CartaTable from "~/components/organisms/CartaTable.vue";

export default {
  name: "App",
  components: {
    CartaTable,
  },
  data() {
    return {
      nowCharactor: "",
      allCharactors: [],
      leftCharactors: [],
    };
  },
  beforeCreate() {
    console.log("fooooooooooooooooooooo");
    this.allCharactors = charactorJson.charactors;
    this.leftCharactors = charactorJson.charactors;
    console.log("🐶");
    console.log(this.allCharactors);
    // 最初の文字を決定
    // this.pickNextChar();
  },
  methods: {
    pickNextChar() {
      // 次の文字をランダムに抽出
      const nextChar =
        this.leftCharactors[
          Math.floor(Math.random() * this.leftCharactors.length)
        ];
      // 抽出した文字を削除
      this.leftCharactors = this.leftCharactors.filter(
        (char) => char !== nextChar
      );
      // 現在の文字に設定
      this.char = nextChar;
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
