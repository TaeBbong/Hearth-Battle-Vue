<template>
  <div class="inputForm">
    <div class="boxArea">
      <div class="inputBox shadow">
        <input type="text" v-model="newScore" placeholder="현재 점수" />
      </div>
    </div>
    <div class="boxArea">
      <div class="inputBox shadow">
        <input type="text" v-model="newFirst" placeholder="1등 횟수" />
      </div>
    </div>
    <div class="boxArea">
      <div class="inputBox shadow">
        <input type="text" v-model="newWin" placeholder="4등 이내 횟수" />
      </div>
    </div>
    <div class="boxArea">
      <div class="inputBox shadow">
        <input type="text" v-model="battleTag" placeholder="닉네임#배틀태그 (선택)" />
      </div>
    </div>
    <div class="submitButton">
      <button class="myButton shadow" v-on:click="calResult">결과보기</button>
    </div>
    <HomeResult v-bind:val="results" v-if="results"></HomeResult>
    <HomeFooter></HomeFooter>
  </div>
</template>

<script>
import HomeResult from "./HomeResult";
import HomeFooter from "./HomeFooter";

export default {
  components: {
    HomeResult: HomeResult
  },
  mounted() {
    console.log("parent mounted!");
    console.log(this.results);
  },
  data() {
    return {
      newScore: null,
      newFirst: null,
      newWin: null,
      battleTag: null,
      isResult: false,
      results: null
    };
  },
  methods: {
    calResult() {
      if (!this.newScore) {
        alert("점수를 입력하세요!");
        return;
      }
      if (!this.newFirst) {
        alert("1등 횟수를 입력하세요!");
        return;
      }
      if (!this.newWin) {
        alert("4등 이내 횟수를 입력하세요!");
        return;
      }
      var score = this.newScore * 1;
      var winGame = this.newWin;
      var firstGame = this.newFirst;
      var battleTag = this.battleTag;
      var winPoint = this.newFirst * 90 + (this.newWin - this.newFirst) * 30;
      var losePoint = winPoint - this.newScore + 4000;
      var loseGame = losePoint / 50;
      var totalPlay = parseInt(loseGame + this.newWin * 1);
      var avgPointPerGame = (((score - 4000) / totalPlay) * 1).toFixed(2);
      var avgRankPerGame = (8 - ((avgPointPerGame * 1 + 90) / 180) * 8).toFixed(
        2
      );
      var winningRate = ((this.newWin / totalPlay) * 100).toFixed(1);
      var estimateRank = parseInt(
        22.8 * Math.pow(11, 9) * Math.pow(2.714, -0.002 * this.newScore)
      );
      if (!this.battleTag) battleTag = "익명";
      this.results = {
        score,
        winGame,
        firstGame,
        battleTag,
        loseGame,
        totalPlay,
        avgPointPerGame,
        avgRankPerGame,
        winningRate,
        estimateRank
      };
      this.isResult = true;
      console.log("calResult done!" + this.results);
      // this.$refs.results.updateCanvasText();
    }
  }
};
</script>

<style scoped>
input:focus {
  outline: #fac3fa;
}
.inputForm {
  text-align: center;
}
.inputBox {
  background: white;
  height: 50px;
  width: 400px;
  display: inline-block;
  line-height: 50px;
  border-radius: 5px;
  margin: 10px 5px 10px 5px;
}
.inputBox input {
  border-style: none;
  font-size: 0.9rem;
  margin: 10px 5px 10px 5px;
}
.submitButton {
  height: 50px;
  border-radius: 5px;
  margin: 10px 5px 10px 5px;
}
.boxArea {
  width: 100%;
}
.myButton {
  background: yellowgreen;
  width: 400px;
  height: 50px;
  border-style: none;
  border-radius: 5px;
  font-size: 0.9rem;
}
</style>>
