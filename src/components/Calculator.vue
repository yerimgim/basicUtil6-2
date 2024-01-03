<template>
  <section>
    <input v-model="calc" class="input-bar" />
    <main class="button-container">
      <button @click="allClear">AC</button>
      <button @click="delCalc">DEL</button>
      <button @click="getOperator" value="%" class="math-symbol-button">
        %
      </button>
      <button @click="getOperator" value="÷" class="math-symbol-button">
        ÷
      </button>
      <button value="7" @click="getNumber">7</button>
      <button value="8" @click="getNumber">8</button>
      <button value="9" @click="getNumber">9</button>
      <button value="×" @click="getOperator" class="math-symbol-button">
        ×
      </button>
      <button value="4" @click="getNumber">4</button>
      <button value="5" @click="getNumber">5</button>
      <button value="6" @click="getNumber">6</button>
      <button value="-" @click="getOperator" class="math-symbol-button">
        -
      </button>
      <button value="1" @click="getNumber">1</button>
      <button value="2" @click="getNumber">2</button>
      <button value="3" @click="getNumber">3</button>
      <button value="+" @click="getOperator" class="math-symbol-button">
        +
      </button>
      <button value="0" @click="getNumber" class="zero-button">0</button>
      <button value="." @click="getPoint">.</button>

      <button @click="getResult" class="math-symbol-button">=</button>
    </main>
  </section>
</template>

<script>
export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: "Calculator",
  data() {
    return {
      calc: "",
      operCheck: true,
      pointCheck: true,
    };
  },
  methods: {
    getNumber(event) {
      const value = event.target.value;
      this.calc += value;
      this.operCheck = true;
    },
    getOperator(event) {
      if (this.operCheck) {
        const value = event.target.value;
        this.calc += value;
        this.operCheck = false;
      }
    },
    getPoint(event) {
      const value = event.target.value;
      if (this.calc.length === 0) {
        return;
      }
      if (this.pointCheck) {
        this.calc += value;
        this.pointCheck = false;
      }
    },
    getResult() {
      const tokens = this.calc.match(/[+\-*/]|\d+\.?\d*/g);
      if (!tokens) return;
      let result = parseFloat(tokens[0]);
      for (let i = 1; i < tokens.length; i += 2) {
        const operator = tokens[i];
        const nextValue = parseFloat(tokens[i + 1]);

        if (isNaN(nextValue)) {
          continue;
        }
        switch (operator) {
          case "+":
            result += nextValue;
            break;
          case "-":
            result -= nextValue;
            break;
          case "*":
            result *= nextValue;
            break;
          case "/":
            if (nextValue === 0) {
              alert("Cannot divide by zero.");
              return;
            }
            result /= nextValue;
            break;
          default:
            break;
        }
      }
      this.calc = String(result);
    },
    delCalc() {
      this.pointCheck = true;
      this.operCheck = true;
      this.calc = this.calc.slice(0, -1);
    },
    allClear() {
      this.pointCheck = true;
      this.calc = "";
    },
  },
};
</script>

<style scoped>
section {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 90vh;
}
.button-container {
  display: grid;
  width: 100%;
  max-width: 500px;
  height: 50%;
  grid-template-columns: repeat(4, 1fr);
  grid-column-gap: 10px;
  grid-row-gap: 10px;
}
button {
  background-color: #f2f3f5;
  border: none;
  color: black;
  font-size: 1.5rem;
  cursor: pointer;
  box-shadow: 3px 3px 3px lightgray;
}
.math-symbol-button {
  font-size: 2rem;
  color: white;
  background-color: orange;
}
.zero-button {
  grid-column: 1/3;
}
.input-bar {
  width: 100%;
  max-width: 500px;
  height: 65px;
  margin-bottom: 10px;
  border-radius: 10px;
  font-size: 30px;
  border: 2px solid #000;
  text-align: right;
  padding-right: 20px;
}
</style>
