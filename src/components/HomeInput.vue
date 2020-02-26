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
    <HomeResult :results="results"></HomeResult>
  </div>
</template>

<script>
import HomeResult from "./HomeResult";

export default {
  components: {
    HomeResult: HomeResult
  },
  data() {
    return {
      newScore: "",
      newFirst: "",
      newWin: "",
      battleTag: "",
      isResult: false,
      results: {}
    };
  },
  methods: {
    calResult() {
      var winPoint = this.newFirst * 90 + (this.newWin - this.newFirst) * 30;
      var losePoint = winPoint - this.newScore + 4000;
      var loseGame = losePoint / 50;
      var totalPlay = loseGame + this.newWin * 1;
      var avgPointPerGame = (this.newScore - 4000) / totalPlay;
      var avgRankPerGame = 8 - ((avgPointPerGame + 90) / 180) * 8;
      var winningRate = (this.newWin / totalPlay) * 100;
      var estimateRank =
        22.8 * Math.pow(11, 9) * Math.pow(2.714, -0.002 * this.newScore);
      console.log(estimateRank);
      this.results = {
        loseGame,
        totalPlay,
        avgPointPerGame,
        avgRankPerGame,
        winningRate,
        estimateRank
      };
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
