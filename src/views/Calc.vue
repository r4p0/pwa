<template>
  <div class="container calc">
    <div>
      <div class="row">
        <div class="col-4 result">{{ num }}</div>
      </div>
      <div class="row panel">
        <div class="col-1-4 button" @click="calculate" data-key="C">AC</div>
        <div class="col-1-4 button" @click="calculate" data-key="del">←</div>
        <div class="col-1-4 button" @click="calculate" data-key="%">%</div>
        <div class="col-1-4 button" @click="calculate" data-key="/">÷</div>
        <div class="col-1-4 button" @click="calculate" data-key="7">7</div>
        <div class="col-1-4 button" @click="calculate" data-key="8">8</div>
        <div class="col-1-4 button" @click="calculate" data-key="9">9</div>
        <div class="col-1-4 button" @click="calculate" data-key="x">×</div>
        <div class="col-1-4 button" @click="calculate" data-key="4">4</div>
        <div class="col-1-4 button" @click="calculate" data-key="5">5</div>
        <div class="col-1-4 button" @click="calculate" data-key="6">6</div>
        <div class="col-1-4 button" @click="calculate" data-key="-">-</div>
        <div class="col-1-4 button" @click="calculate" data-key="1">1</div>
        <div class="col-1-4 button" @click="calculate" data-key="2">2</div>
        <div class="col-1-4 button" @click="calculate" data-key="3">3</div>
        <div class="col-1-4 button" @click="calculate" data-key="+">+</div>
        <div class="col-1-2 button" @click="calculate" data-key="0">0</div>
        <div class="col-1-4 button" @click="calculate" data-key=".">.</div>
        <div class="col-1-4 button" @click="calculate" data-key="=">=</div>
      </div>
    </div>
  </div>
</template>

<script>
import rpn from "./../js/rpn.js";

export default {
  data: () => {
    return {
      num: "0"
    };
  },
  methods: {
    calculate: function(event) {
      let val = event.target.dataset.key;
      this.num = this.num === "0" ? "" : this.num;
      switch (val) {
        case "=":
          this.num = rpn.calCommonExp(this.num);
          break;
        case "C":
          this.num = "";
          break;
        case "del":
          this.num.length = this.num.length > 0 ? this.num.length - 1 : 0;
          break;
        default:
          this.num = this.num + val;
          break;
      }

      this.num = this.num && this.num.toString().length > 0 ? this.num : "0";
    }
  }
};
</script>

<style scoped>
.row {
  box-sizing: border-box;
  width: 100%;
}

.col-1-4,
.col-1-2,
.col-3-4,
.col-1 {
  box-sizing: border-box;
  float: left;
}

.col-1-4 {
  width: 25%;
}

.col-1-2 {
  width: 50%;
}

.col-1 {
  width: 100%;
}

.calc {
  position: absolute;
  top: 71px;
  bottom: 15px;
  left: 15px;
  right: 15px;
  background-color: #f0f0f0;
  box-shadow: 0 2px 2px 0 rgba(0, 0, 0, 0.14), 0 3px 1px -2px rgba(0, 0, 0, 0.2),
    0 1px 5px 0 rgba(0, 0, 0, 0.12);
}

.result {
  position: absolute;
  bottom: 400px;
  font-size: 60px;
  width: 100%;
  text-align: right;
  word-wrap: break-word;
  padding: 20px;
}

.panel {
  position: absolute;
  height: 400px;
  bottom: 0;
  left: 0;
  right: 0;
  border-right: 1px solid #ccc;
  border-bottom: 1px solid #ccc;
}

.button {
  height: 80px;
  font-size: 26px;
  line-height: 80px;
  text-align: center;
  border-top: 1px solid #ccc;
  border-left: 1px solid #ccc;
  background-color: #fff;
  color: #678;
  cursor: pointer;
  -webkit-tap-highlight-color: rgba(178, 179, 182, 0.4);
  user-select: none; /*禁用手机浏览器的用户选择功能 */
}

.button[data-key="="] {
  background-color: #f73;
  color: #fff;
}

.button[data-key="C"] {
  color: #f73;
}
</style>

