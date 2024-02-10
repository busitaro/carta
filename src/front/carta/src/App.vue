<template>
  <button
    type="button"
    @click="startGame"
    class="text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:ring-blue-300 font-medium rounded-lg text-sm px-5 py-2.5 me-2 mb-2 dark:bg-blue-600 dark:hover:bg-blue-700 focus:outline-none dark:focus:ring-blue-800"
  >
    {{ startButtonLabel }}
  </button>
  <CartaTable
    :game-count="gameCount"
    :all-charactors="allCharactors"
    :now-charactor="nowCharactor"
    @correct="chooseCorrect"
  />
  <periodImage v-model="correctImageShow" :img-path="correctImagePath"/>
</template>

<script>
import CartaTable from "~/components/organisms/CartaTable.vue";
import periodImage from "~/components/molecules/PeriodImage.vue";

export default {
  name: "App",
  components: {
    CartaTable,
    periodImage,
  },
  data() {
    return {
      charactorJson: [],
      gameCount: 0,
      nowCharactor: "",
      allCharactors: [],
      leftCharactors: [],
      startButtonLabel: "スタート",
      correctImageShow: false,
      correctImagePath: `${process.env.BASE_URL}assets/images/correct1.png`
    };
  },
  methods: {
    async startGame() {
      await this.getCharactorsJson();
      this.switchResetButtonLabel();
      this.resetCharactors();
      this.pickNextChar();
      this.gameCount++;
    },
    async getCharactorsJson() {
      await fetch(`${process.env.BASE_URL}assets/charactors.json`)
        .then(response => {
          return response.json();
        })
        .then(json => {
          console.log('🍌')
          console.log(json)
          this.charactorJson = json.charactors;
        })
    },
    resetCharactors() {
      this.allCharactors = this.charactorJson;
      this.leftCharactors = this.charactorJson;
      console.log("🍊 reset");
      console.log("↓ allCharactors");
      console.log(this.allCharactors);
      console.log("↓ leftCharactors");
      console.log(this.leftCharactors);
    },
    chooseCorrect() {
      this.correctImageShow = true;
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
    switchResetButtonLabel() {
      this.startButtonLabel = "リセット";
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
