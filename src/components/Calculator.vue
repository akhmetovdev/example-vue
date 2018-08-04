<template>
  <div class="calculator flex-column align-center">
    <div class="flex-row">
      <span class="monitor flex-row justify-end align-center">{{ monitor }}</span>
    </div>
    
    <div class="flex-row">
      <button class="item clear" @click="clear()">CLEAR</button>
      <button class="item remove" @click="remove()">REMOVE</button>
      <button class="item divide" @click="setAction('/')">/</button>
    </div>
    
    <div class="flex-row">
      <button class="item number" @click="concatNumber(7)">7</button>
      <button class="item number" @click="concatNumber(8)">8</button>
      <button class="item number" @click="concatNumber(9)">9</button>
      <button class="item multiply" @click="setAction('*')">X</button>
    </div>
  
    <div class="flex-row">
      <button class="item number" @click="concatNumber(4)">4</button>
      <button class="item number" @click="concatNumber(5)">5</button>
      <button class="item number" @click="concatNumber(6)">6</button>
      <button class="item minus" @click="setAction('-')">-</button>
    </div>
  
    <div class="flex-row">
      <button class="item number" @click="concatNumber(1)">1</button>
      <button class="item number" @click="concatNumber(2)">2</button>
      <button class="item number" @click="concatNumber(3)">3</button>
      <button class="item plus" @click="setAction('+')">+</button>
    </div>
    
    <div class="flex-row">
      <div class="item empty"></div>
      <button class="item number" @click="concatNumber(0)">0</button>
      <div class="item empty"></div>
      <button class="item result" @click="calculate()">=</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Calculator',
  data() {
    return {
      firstNumber: 0,
      secondNumber: 0,
      resultNumber: 0,
      currentNumber: 'firstNumber',
      action: '+'
    };
  },
  computed: {
    monitor() {
      switch (this.currentNumber) {
        case 'firstNumber': {
          return this.firstNumber;
        }
        case 'secondNumber': {
          return `${this.firstNumber} ${this.action} ${this.secondNumber}`;
        }
        case 'resultNumber': {
          return `${this.firstNumber} ${this.action} ${this.secondNumber} = ${
            this.resultNumber
          }`;
        }
        default: {
          return 0;
        }
      }
    }
  },
  methods: {
    clear() {
      this.firstNumber = 0;
      this.secondNumber = 0;
      this.resultNumber = 0;
      this.currentNumber = 'firstNumber';
      this.action = '+';
    },
    remove() {
      if (
        this.currentNumber === 'firstNumber' ||
        this.currentNumber === 'secondNumber'
      ) {
        if (this[this.currentNumber] > 10) {
          this[this.currentNumber] = Math.trunc(this[this.currentNumber] / 10);
        } else {
          this[this.currentNumber] = 0;
        }
      }
    },
    setAction(action) {
      if (this.currentNumber === 'firstNumber') {
        this.action = action;
        this.currentNumber = 'secondNumber';
      }
    },
    concatNumber(number) {
      if (
        this.currentNumber === 'firstNumber' ||
        this.currentNumber === 'secondNumber'
      ) {
        this[this.currentNumber] = this[this.currentNumber] * 10 + number;
      }
    },
    calculate() {
      if (this.currentNumber === 'secondNumber') {
        switch (this.action) {
          case '+': {
            this.resultNumber = this.firstNumber + this.secondNumber;
            break;
          }
          case '-': {
            this.resultNumber = this.firstNumber - this.secondNumber;
            break;
          }
          case '*': {
            this.resultNumber = this.firstNumber * this.secondNumber;
            break;
          }
          case '/': {
            this.resultNumber = this.firstNumber / this.secondNumber;
            break;
          }
          default: {
            this.resultNumber = 0;
            break;
          }
        }
        this.currentNumber = 'resultNumber';
      }
    }
  }
};
</script>

<style scoped lang="scss">
.calculator {
  height: 100vh;
  width: 100vh;
  max-width: 100vw;
  padding: 30px;
}

.flex-row {
  width: 100%;
  height: calc(100% / 6);
}

.item {
  flex: 1;
  flex-basis: 25%;
  overflow: hidden;
  background-color: #84f2d6;
  border: 1px solid #fff6da;
  border-radius: 10px;

  &:hover {
    background-color: #37eabc;
    font-weight: bold;
  }
}

.monitor {
  flex-basis: 100%;
  padding: 10px;
  font-size: calc(((100vh - 60px) / 6 - 20px) / 2);
  line-height: calc(((100vh - 60px) / 6 - 20px) / 2);
  height: calc((100vh - 60px) / 6);
  text-align: right;
}

.clear {
  flex-basis: 50%;
  font-weight: bold;
  font-size: 110%;
}

.remove {
  font-weight: bold;
  font-size: 110%;
}

.divide,
.multiply,
.plus,
.minus {
  font-weight: bold;
  font-size: 110%;
}

.result {
  background-color: #fc6b3f;
  font-weight: bold;
  font-size: 110%;

  &:hover {
    background-color: #fb440d;
  }
}

button {
  padding: 10px;
  border: none;
  cursor: pointer;

  &:focus {
    outline: none;
  }
}
</style>
