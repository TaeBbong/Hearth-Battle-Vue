<template>
  <div>
    <div>
      <canvas id="canvas" ref="canvas" width="673" height="428"></canvas>
    </div>
    <div class="submitButton">
      <button class="myButton shadow" @click="downloadCanvas" id="download">다운로드</button>
    </div>
  </div>
</template>

<script>
import my_battle from "@/assets/전장으로.png";
export default {
  data() {
    return {
      option: {
        fontFamily: "Apple SD Gothic Neo",
        fontSize: 20,
        fontColor: "#FFFFFF",
        fontWeight: "normal"
      },
      props: this.results
    };
  },
  props: ["val"],
  watch: {
    val: {
      immediate: true,
      handler(newVal, oldVal) {
        console.log(newVal);
        console.log(oldVal);
        this.updateCanvas();
      }
    }
  },
  mounted() {
    console.log(this.val);
    this.updateCanvas();
  },
  updated() {
    this.updateCanvas();
  },
  methods: {
    downloadCanvas() {
      const url = this.$refs.canvas.toDataURL("image/png");
      const link = document.createElement("a");
      link.href = url;
      link.setAttribute("download", `전장으로.png`);
      document.body.appendChild(link);
      link.click();
      document.body.removeChild(link);
    },
    updateCanvas() {
      if (!this.$refs.canvas) return;
      this.updateCanvasImage();
    },
    updateCanvasImage() {
      const { canvas } = this.$refs;
      const ctx = canvas.getContext("2d");
      const img = new Image();
      img.src = my_battle;
      img.width = img.width / 3;
      img.height = img.height / 3;
      img.onload = () => {
        ctx.drawImage(img, 0, 0, 673, 428);
        this.updateCanvasText();
      };
    },
    updateCanvasText() {
      console.log("updateText" + this.val);
      var results = this.val;
      const { canvas } = this.$refs;
      const ctx = canvas.getContext("2d");
      String.prototype.format = function() {
        var args = [].slice.call(arguments);
        return this.replace(/(\{\d+\})/g, function(a) {
          return args[+a.substr(1, a.length - 2) || 0];
        });
      };
      var text = "{0}의 전장\n점수: {1}점\n총 플레이 경기: {2}판\n평균 등수: {3}등\n승률: {4}%\n전체 랭킹: {5}등".format(
        results["battleTag"],
        results["score"],
        results["totalPlay"],
        results["avgRankPerGame"],
        results["winningRate"],
        results["estimateRank"]
      );
      console.log(text);
      const { fontFamily, fontSize, fontColor, fontWeight } = this.option;

      ctx.textAlign = "center";
      ctx.textBaseline = "middle";

      // Writing Text
      // 1. user name
      ctx.fillStyle = "#ffffff";
      ctx.font = `${"bold"} ${15}px ${fontFamily}`;
      ctx.fillText(`${results["battleTag"]}`, canvas.width / 2, 66);

      // 2. Other scores
      ctx.font = `${"bold"} ${30}px ${fontFamily}`;
      ctx.fillText(`${results["score"]}`, 145, 228);
      ctx.fillText(`${results["totalPlay"]}`, 270, 228);
      ctx.fillText(`${results["winningRate"]}%`, 405, 228);
      ctx.fillText(`${results["avgRankPerGame"]}`, 533, 228);

      // 3. Estimated Rank
      ctx.font = `${"bold"} ${30}px ${fontFamily}`;
      ctx.fillText(`${results["estimateRank"]}등`, 405, 325);

      // 4. Date
      ctx.font = `${"bold"} ${13}px ${fontFamily}`;
      var today = new Date();
      var myToday =
        today.getFullYear() +
        "년 " +
        (today.getMonth() + 1) +
        "월 " +
        today.getDate() +
        "일";
      ctx.fillText(myToday, canvas.width / 2, 128);
    }
  }
};
</script>

<style>
.myButton {
  background: burlywood;
  width: 300px;
  height: 50px;
  border-style: none;
  border-radius: 5px;
  font-size: 0.9rem;
}
.submitButton {
  height: 50px;
  border-radius: 5px;
  margin: 10px 5px 10px 5px;
}
</style>