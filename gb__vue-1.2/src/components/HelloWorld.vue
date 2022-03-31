<template>
  <div class="hello">
    <h1>{{ msg }}</h1>

    <!-- <hr /> -->

    <div class="display">
      <input v-model.number="operand1" type="number" />
      <input v-model.number="operand2" type="number" />
    </div>

    <div class="keyboard">
      <!-- :disabled="getBtnStatusDisabled(operand)" -->

      <button
        v-for="(operand, idx) in operands"
        :key="operand"
        :name="operand"
        :id="idx + 1"
        class="btns"
        @click="calculate(operand)"
      >
        {{ operand }}
      </button>

      <!-- <button @click="calculate('+')">+</button>
      <button @click="calculate('-')">-</button>
      <button @click="calculate('/')">/</button> -->
      <!-- <button @click="calculate('/')" :disabled="operand2 === 0">/</button> -->
      <!-- <button @click="calculate('*')">*</button>
      <button @click="exponentiation(operand1, operand2)">x²</button>
      <button @click="integerDivision(operand1, operand2)">integer</button> -->
    </div>

    <p class="result">{{ result }}</p>

    <div class="errors" v-if="error">Ошибка: {{ error }}</div>
    <!-- <div class="errors" v-show="error">Ошибка: {{ error }}</div> -->

    <div class="strange-message">
      <template v-if="result < 0">Получилось отрицательное число</template>
      <template v-else-if="result < 100">Результат в первой сотне</template>
      <template v-else>Получилось слишком большое число</template>
    </div>

    <div>____________</div>
    <br />

    <div class="arr">
      <div v-for="(item, index) in myCollection" :key="index">
        {{ index }} - {{ item }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  props: {
    msg: {
      type: String,
      default: "Empty Props",
      // required: true,
    },
  },
  data() {
    return {
      message: "Hello Vue",
      myCollection: [1, 2, 3, 4, 5, 6],
      operands: ["+", "-", "/", "*"],
      operand1: 0,
      operand2: 0,
      error: "",
      result: 0,
    };
  },
  methods: {
    calculate(operation = "+") {
      this.error = "";
      switch (operation) {
        case "+":
          this.add();
          break;
        case "-":
          this.substract();
          break;
        case "/":
          this.divide();
          break;
        case "*":
          this.multyply();
          break;
      }
    },
    add() {
      this.result = this.operand1 + this.operand2;
    },
    substract() {
      this.result = this.operand1 - this.operand2;
    },
    doThat(str, evnt) {
      console.log("click", str, evnt);
    },
    onValidate() {
      console.log("validation true");
    },
    divide() {
      if (this.operand2 === 0) {
        this.error = "На ноль делить нельзя!";
        return;
      } else {
        this.result = this.operand1 / this.operand2;
      }
    },
    multyply() {
      const { operand1, operand2 } = this;
      this.result = operand1 * operand2;
    },
    // возводит число в заданную степень
    exponentiation(op1, op2) {
      this.result = Math.pow(op1, op2);
    },
    // целочисленное деление
    integerDivision(op1, op2) {
      let intResult = op1 / op2;
      this.result = Math.trunc(intResult);
    },
    // Disabled кнопку, когда деление на 0
    getBtnStatusDisabled(operation) {
      if (operation === "/" && this.operand2 === 0) {
        return true;
      }
      return false;
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.hello {
  width: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
}
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
button {
  min-width: 40px;
  height: 30px;
  margin: 15px;
}
input {
  padding: 8px;
  margin: 5px;
}
.result {
  font-size: 25px;
  width: 100%;
  text-align: center;
  border: 2px solid black;
}
</style>
