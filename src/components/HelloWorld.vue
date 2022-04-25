<template>
  <div class="hello">
    <h1>{{ msg }}</h1>

    <input v-model.number="operand1" />
    <input v-model.number="operand2" />

    <h1 v-if="!err">
      Результат {{ operand1 }} {{ sign }} {{ operand2 }} равен {{ result }}
    </h1>
    <h1 v-else-if="err">На ноль делить нельзя</h1>
    <h1 v-else>
      Результат {{ operand1 }} {{ sign }} {{ operand2 }} равен {{ result }}
    </h1>

    <div class="sign">
      <button
        v-for="operand in operands"
        :key="operand"
        @click="calculate(operand)"
      >
        {{ operand }}
      </button>
    </div>
    <input
      type="checkbox"
      name="showKeyBoard"
      id="keyboard"
      @change="visible = !visible"
    />
    <label for="keyboard">Показать\Скрыть клавиатуру </label>
    <button @click="clear">Сброс</button>
    <hr />
    <br />

    <div class="Keyboard" v-show="visible">
      <div class="selectOperand">
        <input
          type="radio"
          id="operand1"
          value="operand1"
          name="operand"
          @change="focusField"
          checked
        />
        <label for="operand1"> operand1</label>
        <input
          type="radio"
          id="operand2"
          value="operand2"
          name="operand"
          @change="focusField"
        />
        <label for="operand2"> operand2</label>
      </div>

      <!-- Конопки от 1 до 0 -->
      <div class="calculateNumber">
        <button
          v-for="number in numbersCalculate"
          :key="number"
          @click="valueCalculate(number)"
        >
          {{ number }}
        </button>
      </div>
    </div>
    <!-- ЛОГИ -->
    <!-- <div class="logs" v-for="log in logs" :key="log">
      <div class="log">{{ log }}</div>
    </div> -->
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  props: {
    msg: {
      type: String,
    },
  },

  data() {
    return {
      operands: ["+", "-", "/", "*", "^"],
      operand1: "",
      operand2: "",
      result: 0,
      sign: "",
      arr: [],
      err: false,
      numbersCalculate: [
        "1",
        "2",
        "3",
        "4",
        "5",
        "6",
        "7",
        "8",
        "9",
        "0",
        "delete",
      ],
      checkedInput: "operand1",
      str: "",
      visible: true,
      // logs: {},
    };
  },

  methods: {
    clear() {
      this.operand1 = "";
      this.operand2 = "";
    },
    focusField(event) {
      this.checkedInput = event.target.value;
      console.log(this.checkedInput);
    },
    // примает и выводит значение нажатой цифры калькулятора
    valueCalculate(value) {
      // проверка какую кнопку калькулятора нажали если delete удаляем символы если иначе меняем значение operand1 или operand1
      if (value == "delete") {
        if (this.checkedInput == "operand1") {
          this.operand1 = String(this.operand1);
          this.str = this.operand1.length;
          if (this.str != 0) {
            this.operand1 = this.operand1.slice(0, -1);
            this.operand1 = parseInt(this.operand1);
            console.log(this.operand1);
          }
        } else {
          this.operand2 = String(this.operand2);
          this.operand2 = this.operand2.slice(0, -1);
          this.operand2 = parseInt(this.operand2);
        }
      } else if (this.checkedInput == "operand1") {
        this.operand1 += value;
        this.operand1 = parseInt(this.operand1);
      } else {
        this.operand2 += value;
        this.operand2 = parseInt(this.operand2);
      }
    },

    test(event) {
      console.log(event);
    },

    calculate(operation = "+") {
      this.error = "";
      if (this.operand1 === "" || this.operand2 === "") {
        alert("Поля должны содержать цифры ");
      }
      switch (operation) {
        case "+":
          this.summation();
          break;

        case "-":
          this.substraction();
          break;

        case "/":
          this.didviding();
          break;

        case "*":
          this.multiplication();
          break;

        case "^":
          this.exponentiation();
          break;
      }
      // this.logs[Date.now()] = `${this.operand1} ${this.sign} ${this.operand1}`;
      // const key = Date.now();
      // const value = `${this.operand1} ${this.sign} ${this.operand1}`;
      // this.$set(this.logs, key, value);
    },

    summation() {
      console.log(this.operand1, this.operand2);
      this.result = this.operand1 + this.operand2;
      this.sign = "+";
    },
    substraction() {
      this.result = this.operand1 - this.operand2;
      this.sign = "-";
    },
    didviding() {
      this.sign = "/";
      const { operand1, operand2 } = this;
      if (operand2 === 0) {
        this.err = true;
      } else {
        this.err = false;
        this.result = operand1 / operand2;
      }
    },
    multiplication() {
      this.result = this.operand1 * this.operand2;
      this.sign = "*";
    },
    exponentiation() {
      this.result = Math.pow(this.operand1, this.operand2);
      this.sign = "^";
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
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
  width: inherit;
}
</style>
