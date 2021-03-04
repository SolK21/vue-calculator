<template>
  <div class="calculator">
    <div class="display">{{current || tmpOutcome || '0'}}</div>
    <div @click="clear" class="btn">AC</div>
    <div @click="changeSign" class="btn">+/-</div>
    <div @click="percentage" class="btn">%</div>
    <div @click="operation('/')" class="btn operator">/</div>
    <div @click="input('7')" class="btn">7</div>
    <div @click="input('8')" class="btn">8</div>
    <div @click="input('9')" class="btn">9</div>
    <div @click="operation('*')" class="btn operator">x</div>
    <div @click="input('4')" class="btn">4</div>
    <div @click="input('5')" class="btn">5</div>
    <div @click="input('6')" class="btn">6</div>
    <div @click="operation('-')" class="btn operator">-</div>
    <div @click="input('1')" class="btn">1</div>
    <div @click="input('2')" class="btn">2</div>
    <div @click="input('3')" class="btn">3</div>
    <div @click="operation('+')" class="btn operator">+</div>
    <div @click="input('0')" class="btn zero">0</div>
    <div @click="input('.')" class="btn">,</div>
    <div @click="operation('=')" class="btn operator">=</div>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
//for tommorow fix percentage
@Component
export default class Calculator extends Vue {
  
  current = '';
  tmpOutcome = 0;
  operator = '+';

  finalResult = 0;

  isFirst = true;
  

  clear() {
    this.current = '';
    this.tmpOutcome = 0;
    this.operator = '+';

    
  }

  operation(symbol: string) {
    switch (this.operator) {
      case '+':
        this.tmpOutcome += +this.current;
        break;

      case '-':
        this.tmpOutcome -= +this.current;
        break;

      case '*':
        this.tmpOutcome *= +this.current;
        break;

      case '/':
        this.tmpOutcome /= +this.current;
        break;
    
      default:
        break;
    }

    this.operator = symbol;
    this.current = '';
    
  }

  input(char: string) {
    this.current = this.current + char;
  }

  changeSign() {
    if (this.current != '') {
      this.current = (+this.current * (-1)).toString();
    } else {
      this.tmpOutcome *= -1;
    }
    
  }

  percentage() {
    this.current = (+this.current / 100).toString();
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped >

.calculator {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
  font-size: 40px;
  width: 400px;
  margin: 0 auto;
}

.display {
  grid-column: 1/5;
  background-color: #333;
  color: white;
}

.zero {
  grid-column: 1/3;
}

.btn {
  border-color: #f2f2f2;
  border: 1px solid #999;
  cursor: pointer;
  
}
.btn:hover {
  background-color: rgb(136, 134, 134);
  color: white;
}

.operator {
  background-color: orange;
  color: white;
}
</style>
