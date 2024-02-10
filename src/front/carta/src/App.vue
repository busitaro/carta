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
    @incorrect="chooseIncorrect"
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
      this.playYomifuda(this.nowCharactor);
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
      // 文字はランダム
      this.allCharactors = this.charactorJson;
      this.allCharactors = this.allCharactors.sort(() => Math.random() - 0.5)
      // まだとられていない文字
      this.leftCharactors = this.charactorJson;
      console.log("🍊 reset");
      console.log("↓ allCharactors");
      console.log(this.allCharactors);
      console.log("↓ leftCharactors");
      console.log(this.leftCharactors);
    },
    async chooseCorrect() {
      const sleep = msec => new Promise(resolve => setTimeout(resolve, msec));

      // 正解の表示
      this.playCorrectSound();
      this.correctImageShow = true;
      await sleep(2000);

      this.pickNextChar();
      if (this.nowCharactor) {
        this.playYomifuda(this.nowCharactor);
      }
    },
    chooseIncorrect() {
      this.playIncorrectSound();
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
    playYomifuda(char) {
      const audio = new Audio(process.env.BASE_URL + `assets/sounds/${char}.mp3`)
      audio.play();
    },
    playCorrectSound() {
      const audio = new Audio(process.env.BASE_URL + `assets/sounds/correct.mp3`)
      audio.play()
    },
    playIncorrectSound() {
      const audio = new Audio(process.env.BASE_URL + `assets/sounds/incorrect.mp3`)
      audio.play()
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
