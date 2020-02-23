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
        <input type="text" v-model="newTime" placeholder="플레이 시간" />
      </div>
    </div>
    <div class="submitButton">
      <button class="myButton shadow" v-on:click="calResult">결과보기</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newScore: "",
      newFirst: "",
      newWin: "",
      newTime: ""
    };
  },
  methods: {
    calResult() {
      console.log(this.newScore, this.newFirst, this.newWin, this.newTime);
      return this.newScore;
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
