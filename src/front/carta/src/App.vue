<template>
  <button
    type="button"
    @click="startGame"
    class="text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:ring-blue-300 font-medium rounded-lg text-sm px-5 py-2.5 me-2 mb-2 dark:bg-blue-600 dark:hover:bg-blue-700 focus:outline-none dark:focus:ring-blue-800"
  >
    スタート
  </button>
  <CartaTable
    :all-charactors="allCharactors"
    :now-charactor="nowCharactor"
    @correct="chooseCorrect"
  />
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
  created() {
    this.allCharactors = charactorJson.charactors;
    this.leftCharactors = charactorJson.charactors;
  },
  methods: {
    startGame() {
      this.pickNextChar();
    },
    chooseCorrect() {
      this.pickNextChar();
    },
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
      this.nowCharactor = nextChar;
      // コンソール出力
      console.log(`🍇 現在の文字「${this.nowCharactor}」`);
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
  margin-top: 30px;
}
</style>
