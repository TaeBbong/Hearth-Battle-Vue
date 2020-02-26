<template>
  <div>
    <canvas id="canvas" ref="canvas" width="600" height="473"></canvas>
    <button @click="downloadCanvas" id="download">다운로드</button>
  </div>
</template>

<script>
import battle from "@/assets/battle.jpeg";
export default {
  data() {
    return {
      option: {
        fontFamily: "Gulim",
        fontSize: 30,
        fontColor: "#FFFFFF",
        fontWeight: "normal"
      }
    };
  },
  props: ["results"],
  mounted() {
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
    updateCanvas(results) {
      if (!this.$refs.canvas) return;
      this.updateCanvasImage(results);
    },
    updateCanvasImage(results) {
      const { canvas } = this.$refs;
      const ctx = canvas.getContext("2d");
      const img = new Image();
      img.src = battle;
      img.onload = () => {
        ctx.drawImage(img, 0, 0);
        this.updateCanvasText(results);
      };
    },
    updateCanvasText(results) {
      console.log(results);
      const { canvas } = this.$refs;
      const ctx = canvas.getContext("2d");
      String.prototype.format = function() {
        var args = [].slice.call(arguments);
        return this.replace(/(\{\d+\})/g, function(a) {
          return args[+a.substr(1, a.length - 2) || 0];
        });
      };
      var text = "{0}의 전장\n총 플레이 경기: {1}\n평균 등수: {2}\n승률: {3}\n전체 랭킹: {4}".format(
        results["battleTag"],
        results["totalPlay"],
        results["avgRankPerGame"],
        results["winningRate"],
        results["estimateRank"]
      );
      console.log(text);
      const { fontFamily, fontSize, fontColor, fontWeight } = this.option;

      ctx.textAlign = "center";
      ctx.textBaseline = "middle";
      ctx.font = `${fontWeight} ${fontSize}px ${fontFamily}`;

      const lines = text.split("\n");
      lines.forEach((line, index) => {
        ctx.fillStyle = fontColor;
        ctx.fillText(
          line,
          canvas.width / 2,
          canvas.height - fontSize * (lines.length - index) * 1.5
        );
      });
    }
  }
};
</script>

<style>
</style>