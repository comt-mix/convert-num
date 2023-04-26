<template>
  <div id="app">
    <div class="container">
      <div class="box">
        <input
          v-model="num"
          type="text"
          maxlength="42"
          placeholder=""
          oninput="this.value = this.value.replace(/[^0-9]/g, '').replace(/(\d)(?=(\d{3})+(?!\d))/g, '$1,');"
        />
        <button @click="convertNum">확인</button>
        <button @click="clearNum">초기화</button>
      </div>
      <div class="convert">
        <div class="bottom-line">{{ translate }}</div>
        <div class="bottom-text">원</div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      num: "",
      translate: "",
    };
  },
  methods: {
    convertNum() {
      const digits = [
        "",
        "일",
        "이",
        "삼",
        "사",
        "오",
        "육",
        "칠",
        "팔",
        "구",
        "십",
      ];
      const units = [
        "",
        "십",
        "백",
        "천",
        "",
        "십",
        "백",
        "천",
        "",
        "십",
        "백",
        "천",
        "",
        "십",
        "백",
        "천",
        "",
        "십",
        "백",
        "천",
        "",
        "십",
        "백",
        "천",
        "",
        "십",
        "백",
        "천",
        "",
        "십",
        "백",
        "천",
      ];
      const tempStr = this.num.replaceAll(",", "");
      const numStr = tempStr.replace(/(^0+)/, "");

      let result = "";

      for (let i = 0; i < numStr.length; i++) {
        let str = "";
        let han = digits[numStr.charAt(numStr.length - (i + 1))];

        if (han !== "") str += han + units[i];

        if (i === 4) str += "만";
        if (i === 8) str += "억";
        if (i === 12) str += "조";
        if (i === 16) str += "경";
        if (i === 20) str += "해";
        if (i === 24) str += "자";
        if (i === 28) str += "양";

        result = str + result;
      }
      //0,012,131,546
      //

      return (this.translate = result);
    },
    clearNum() {
      this.num = "";
      this.translate = "";
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
  margin-top: 60px;
}
button {
  padding: 0.6rem;
  border-style: none;
  border-radius: 0.4rem;
  color: white;
  background-color: #5b96fb;
  margin-right: 0.4rem;
}
input {
  width: 40%;
  padding: 0.6rem;
  margin-right: 0.4rem;
  border-radius: 0.4rem;
  border: 1.4px solid #448aff;
  color: #9e9e9e;
}
.box {
  margin: 0 auto;
  margin-bottom: 4rem;
  border-radius: 0.6rem;
}
.convert {
  display: flex;
  justify-content: center;
}
.bottom-line {
  width: 72%;
  border-bottom: 2px dotted #448aff;
  color: #9e9e9e;
  font-weight: bold;
}
.bottom-text {
  color: #448aff;
  font-weight: bold;
}
</style>
