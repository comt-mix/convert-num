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
      const hanA = [
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
      const danA = [
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
      const numStr = this.num.replaceAll(",", "");
      let result = "";

      for (let i = 0; i < numStr.length; i++) {
        let str = "";
        let han = hanA[numStr.charAt(numStr.length - (i + 1))];

        if (han !== "") str += han + danA[i];

        if (i == 4) str += "만";
        if (i == 8) str += "억";
        if (i == 12) str += "조";
        if (i == 16) str += "경";
        if (i == 20) str += "해";
        if (i == 24) str += "자";
        if (i == 28) str += "양";

        result = str + result;
      }

      return (this.translate = result);
    },
    clearNum() {
      this.num = "";
      this.translate = "";
    },
  },
  // methods: {
  //   convertNum() {
  //     const digits = [
  //       "영",
  //       "일",
  //       "이",
  //       "삼",
  //       "사",
  //       "오",
  //       "육",
  //       "칠",
  //       "팔",
  //       "구",
  //     ];
  //     //십만부터 천만은 뒤에 계속해서 만이 붙어서 지웠음.
  //     const units = [
  //       "",
  //       "십",
  //       "백",
  //       "천",
  //       "만",
  //       "십",
  //       "백",
  //       "천",
  //       "억",
  //       "십억",
  //       "백",
  //       "천",
  //       "조",
  //       "십",
  //       "백",
  //       "천",
  //       "경",
  //       "십",
  //       "백",
  //       "천",
  //       "해",
  //       "십",
  //       "백",
  //       "천",
  //       "자",
  //       "십",
  //       "백",
  //       "천",
  //       "양",
  //       "십",
  //       "백",
  //       "천",
  //     ];
  //     //comma 추가로 인해 텍스트 변환에러. 변환 전 comma빼고 변환하기
  //     let result = "";
  //     const numStr = this.num.replaceAll(",", "");
  //     const numLen = numStr.length;

  //     if (numLen === 0) window.alert("금액을 입력해주세요!");

  //     for (let i = 0; i < numLen; i++) {
  //       const digit = parseInt(numStr.charAt(i));
  //       const unit = units[numLen - i - 1];

  //       if (numStr.charAt(i) !== 0 && numStr.charAt(i + 1) === 0) {
  //         result += digits[digit];
  //         console.log(11111111);
  //       }

  //       //1. 마지막 숫자가 1일경우
  //       //2. 숫자가 1이고
  //       if (i === numLen - 1 && digit === 1) {
  //         result += "일";
  //       } else if (digit !== 0) {
  //         result += digits[digit] + unit;
  //       } else if (i === numLen - 5) {
  //         //1. 십만 단위에서는 '만'을 붙이지 않도록
  //         //2. 천만원 이후부터 억만 십업만 등의 단위는 존재하지 않으므로
  //         // numLen < 9조건을 추가해서 천만원이 넘어가면 만을 없앴음.
  //         result += "만";
  //         //여기 고치기
  //       }
  //     }
  //     //뒷자리가 0이면 단위를 끊어주기 continue
  //     //뒷자리에 숫자가 오면 단위 빼기

  //     return (this.translate = result);
  //   },

  // },
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
