<template>
  <div>
    <h2>Calculator</h2>
    <input v-model="expression" placeholder="..." />
    <button @click="computeResult">Calculate</button>
    <p>Result: {{ result }}</p>
  </div>
</template>

<script>
export default {
  name: "NewCalculator",
  data() {
    return {
      expression: "",
      result: null,
    };
  },
  methods: {
    createTreeNode(value) {
      return {
        value: value || "",
        left: null,
        right: null,
      };
    },
    parseExpression(expression) {
      const precedence = {
        "+": 1,
        "-": 1,
        "*": 2,
        "/": 2,
      };
      const operators = [];
      const operands = [];
      for (let i = 0; i < expression.length; i++) {
        let ch = expression[i];
        if (ch === " ") continue;

        if (ch >= "0" && ch <= "9") {
          let num = 0;
          while (
            i < expression.length &&
            expression[i] >= "0" &&
            expression[i] <= "9"
          ) {
            num = num * 10 + (expression[i] - "0");
            i++;
          }
          i--;
          operands.push(this.createTreeNode(num));
        } else if (ch === "(") {
          operators.push(ch);
        } else if (ch === ")") {
          while (
            operators.length > 0 &&
            operators[operators.length - 1] !== "("
          ) {
            let op = operators.pop();
            let right = operands.pop();
            let left = operands.pop();
            let node = this.createTreeNode(op);
            node.left = left;
            node.right = right;
            operands.push(node);
          }
          operators.pop();
        } else {
          while (
            operators.length > 0 &&
            precedence[ch] <= precedence[operators[operators.length - 1]]
          ) {
            let op = operators.pop();
            let right = operands.pop();
            let left = operands.pop();
            let node = this.createTreeNode(op);
            node.left = left;
            node.right = right;
            operands.push(node);
          }
          operators.push(ch);
        }
      }

      while (operators.length > 0) {
        let op = operators.pop();
        let right = operands.pop();
        let left = operands.pop();
        let node = this.createTreeNode(op);
        node.left = left;
        node.right = right;
        operands.push(node);
      }

      return operands.pop();
    },
    calculate(node) {
      if (!node.left && !node.right) {
        return node.value;
      }

      let leftVal = this.calculate(node.left);
      let rightVal = this.calculate(node.right);

      switch (node.value) {
        case "+":
          return leftVal + rightVal;
        case "-":
          return leftVal - rightVal;
        case "*":
          return leftVal * rightVal;
        case "/":
          return leftVal / rightVal;
        default:
          return 0;
      }
    },
    computeResult() {
      let root = this.parseExpression(this.expression);
      this.result = this.calculate(root);
    },
  },
};
</script>

<style></style>
