<template>
  <div>
    <div class="inputBox shadow">
      <input type="text" v-model="newScore" placeholder="현재 점수" />
    </div>
    <div class="inputBox shadow">
      <input type="text" v-model="newFirst" placeholder="1등 횟수" />
    </div>
    <div class="inputBox shadow">
      <input type="text" v-model="newWin" placeholder="4등 이내 횟수" />
    </div>
    <div class="inputBox shadow">
      <input type="text" v-model="newTime" placeholder="플레이 시간" />
    </div>
    <div class="submitButton">
      <button v-on:click="calResult">결과보기</button>
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
    }
  }
};
</script>

<style scoped>
input:focus {
  outline: none;
}
.inputBox {
  background: white;
  height: 50px;
  line-height: 50px;
  border-radius: 5px;
}
.inputBox input {
  border-style: none;
  font-size: 0.9rem;
}
.submitButton {
  height: 50px;
  border-radius: 5px;
}
</style>>
