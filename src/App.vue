<template>
  <div id="app">
    <div class="container">
      <div class="box">
        <input
          v-model="num"
          type="text"
          maxlength="17"
          placeholder="최대 거래액은 1조입니다."
          oninput="this.value = this.value.replace(/^0+|\D+/g, '').replace(/(\d)(?=(?:\d{3})+(?!\d))/g, '$1,');"
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
      let result = "";
      const digits = [
        "영",
        "일",
        "이",
        "삼",
        "사",
        "오",
        "육",
        "칠",
        "팔",
        "구",
      ];
      //십만부터 천만은 뒤에 계속해서 만이 붙어서 지웠음.
      const units = [
        "",
        "십",
        "백",
        "천",
        "만",
        "십",
        "백",
        "천",
        "억",
        "십억",
        "백억",
        "천억",
        "조",
      ];
      //comma 추가로 인해 텍스트 변환에러. 변환 전 comma빼고 변환하기.
      let numStr = this.num.replaceAll(",", "");
      let numLen = numStr.length;

      if (numLen === 0) window.alert("금액을 입력해주세요!");

      for (let i = 0; i < numLen; i++) {
        //입력이 text로 string이어서 charAt을 이용한 이후 추후 숫자비교를 위해 parseInt사용.
        //parseInt와 number의 차이점
        //parseInt는 숫자로 된 문자열을 정수로 변환해주는 것. 그 외 값은 NaN 리턴
        //number는 숫자로 된 문자열 전체를 변환. 그 외 값은 NaN 리턴

        //for문을 이용해서 0부터 charAt에 들어감. 그럼 제일 앞인 인덱스0부터 비교해서
        //하나씩 차례대로 숫자로 변환돼서 digit에 들어가게 됨.
        //digit은 입력한 값에서 i번째 자릿수 숫자
        let digit = parseInt(numStr.charAt(i));

        //전체 길이에서 -1을 해야 인덱스 순서가 맞음. 거기에 i씩 더 빼주게 되면
        //전체 길이에서 1씩 줄어들게 됨 4,3,2,1,0 이런식으로
        //unit은 i번째 자릿수 단위를 units에서 찾아서 반환()
        //4(만) 3(천) 2(백) 1(십) 0("")
        let unit = units[numLen - i - 1];

        // 일의 자리인 경우에는 숫자를 그대로 한글로 변환
        if (i === numLen - 1 && digit === 1 && numLen !== 1) {
          result += "일";
        } else if (digit !== 0) {
          console.log(digit, unit);
          // 일의 자리가 아니거나 숫자가 0이 아닐 경우
          result += digits[digit] + unit;
        } else if (i === numLen - 5) {
          // 십만 단위에서는 '만'을 붙이지 않습니다.
          result += "만";
        }
      }

      return (this.translate = result);
    },
    clearNum() {
      this.num = "";
      this.translate = "";
    },
  },
  filters: {
    comma(v) {
      return String(v)
        .replace(/[^0-9]/g, "")
        .replace(/\B(?=(\d{3})+(?!\d))/g, ",");
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
  padding: 0.6rem;
  margin-right: 0.4rem;
  border-radius: 0.4rem;
  border: 1.4px solid #448aff;
  color: #9e9e9e;
}
.box {
  width: 30%;
  margin: 0 auto;
  margin-bottom: 1.5rem;
  border-radius: 0.6rem;
}
.convert {
  display: flex;
  justify-content: center;
}
.bottom-line {
  width: 22%;
  border-bottom: 2px dotted #448aff;
  color: #9e9e9e;
  font-weight: bold;
}
.bottom-text {
  color: #448aff;
  font-weight: bold;
}
</style>
