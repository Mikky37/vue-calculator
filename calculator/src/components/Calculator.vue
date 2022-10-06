<template>
  <div class="calculator">
    <div class="display">{{answer || 0}}</div>
    <div @click="clear" class="btn">C</div>
    <div @click="negate" class="btn">+/-</div>
    <div @click="percent" class="btn">%</div>
    <div @click="divide" class="btn operator">/</div>
    <div @click="append('7')" class="btn">7</div>
    <div @click="append('8')" class="btn">8</div>
    <div @click="append('9')" class="btn">9</div>
    <div @click="multiply" class="btn operator">X</div>
    <div @click="append('4')" class="btn">4</div>
    <div @click="append('5')" class="btn">5</div>
    <div @click="append('6')" class="btn">6</div>
    <div @click="subtract" class="btn operator">-</div>
    <div @click="append('1')" class="btn">1</div>
    <div @click="append('2')" class="btn">2</div>
    <div @click="append('3')" class="btn">3</div>
    <div @click="add" class="btn operator" >+</div>
    <div @click="append('0')" class="btn zero">0</div>
    <div @click="dot" class="btn">.</div>
    <div @click="equal" class="btn operator">=</div>
  </div>
</template>

<script>
export default {
  name: 'CalculatorCode',
  data() {
    return {
      answer: '',
      operator: null,
      previous: null,
      operatorClicked: false
    }
  },
  methods: {
    clear() {
      this.answer = ''
    },
    negate() {
      this.answer = this.answer.charAt(0) === '-' ? this.answer.slice(1) : `-${this.answer}` 
    },
    percent() {
      this.answer = `${parseFloat(this.answer)/100}`
    },
    append(number) {
      if (this.operatorClicked) {
        this.answer = '';
        this.operatorClicked = false;
      }
      this.answer = `${this.answer}${number}`
    },
    dot() {
      if (this.answer.indexOf('.') === -1) {
        this.append('.')
      }
    },
    setPrevious() {
      this.previous = this.answer;
      this.operatorClicked = true
    },
    divide() {
      this.operator = (a, b) => a / b;
      this.setPrevious()
    },
    multiply() {
      this.operator = (a, b) => a * b;
      this.setPrevious()
    },
    subtract() {
      this.operator = (a, b) => a - b;
      this.setPrevious()
    },
    add() {
      this.operator = (a, b) => a + b;
      this.setPrevious()
    },
    equal() {
      this.answer = `${this.operator(
        parseFloat(this.previous), 
        parseFloat(this.answer)
      )}`;
      this.previous = null
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.calculator{
  font-size: 40px;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
  display: grid;
  margin: 0 auto;
  width: 400px;
}
.display{
  grid-column: 1 / 5;
  background-color: #333;
  color: white;
}
.zero{
  grid-column: 1 / 3;
}
.btn{
  background-color: #f2f2f2;
  border: 1px solid #999;
  cursor: pointer;
}
.btn:active{
  transform: scale(0.95);
}
.operator{
  background-color: orange;
  color: white;
}
</style>
