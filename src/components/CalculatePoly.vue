<template>
  <div>
    <h2>simplify Polynomial</h2>
    <input v-model="expression" placeholder="x^2+3x^2" />
    <button @click="computeResult">Simplify</button>
    <p>Result: {{ result }}</p>
  </div>
</template>

<script>
export default {
  name: "CalculatePoly",
  data() {
    return {
      expression: "",
      result: null,
    };
  },
  methods: {
    simplifyPoly(poly) {
      const terms = poly.match(/-?\d*x\^\d+|-?\d*x\^\d+|-?x\^\d+/g);
      const coefficients = {};

      terms.map((term) => {
        let [coefficient, exponent] = term.split("x^");

        if (coefficient === "" || coefficient === "-") {
          coefficient = coefficient === "-" ? -1 : 1;
        } else {
          coefficient = parseInt(coefficient, 10);
        }

        exponent = parseInt(exponent, 10);

        coefficients[exponent] = coefficients[exponent]
          ? coefficients[exponent] + coefficient
          : coefficient;
      });

      let result = "";
      Object.keys(coefficients)
        .sort((a, b) => a - b)
        .forEach((exponent) => {
          const coef = coefficients[exponent];

          if (coef !== 0) {
            if (coef === 1) {
              result += (result ? "+" : "") + "x^" + exponent;
            } else if (coef === -1) {
              result += "-x^" + exponent;
            } else {
              result +=
                (result && coef > 0 ? "+" : "") + coef + "x^" + exponent;
            }
          }
        });
      return result;
    },
    computeResult() {
      this.result = this.simplifyPoly(this.expression);
    },
  },
};
</script>
