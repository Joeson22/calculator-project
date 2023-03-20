<template>
  <div class="calculator">
    <div class="display">{{ current || 0 }}</div>
    <div @click="clear" class="btn">AC</div>
    <div @click="sign" class="btn">+/-</div>
    <div @click="percent" class="btn">%</div>
    <div @click="divide" class="btn operator">÷</div>
    <div @click="append(7)" class="btn">7</div>
    <div @click="append(8)" class="btn">8</div>
    <div @click="append(9)" class="btn">9</div>
    <div @click="multiply" class="btn operator">x</div>
    <div @click="append(4)" class="btn">4</div>
    <div @click="append(5)" class="btn">5</div>
    <div @click="append(6)" class="btn">6</div>
    <div @click="subtract" class="btn operator">-</div>
    <div @click="append(1)" class="btn">1</div>
    <div @click="append(2)" class="btn">2</div>
    <div @click="append(3)" class="btn">3</div>
    <div @click="add" class="btn operator">+</div>
    <div @click="append(0)" class="zero btn">0</div>
    <div @click="dot" class="btn">.</div>
    <div @click="equal" class="btn operator">=</div>
    
  </div>
</template>

<script>


export default {
  name: 'calculator-comp',
  data() {
    return {
      current: '',
      previous: null,
      operatorClicked: false,
      operator: null,
    }
  },
  methods: {
    clear() {
      this.current = '';
    },
    sign () {
      this.current = this.current.charAt(0) === '-' ? this.current.slice(1) : `-${this.current}`;
    },
    percent() {
      // this.current = this.current/100
      this.current = `${parseFloat(this.current) / 100}`
    },
    append(number) {
      if(this.operatorClicked) {
        this.current = '';
        this.operatorClicked = false;
      }
      // if(!this.operatorClicked) {
      //   this.current = `${this.current}${number}`
      // }
      this.current = `${this.current}${number}`
    },
    dot() {
      if (this.current.indexOf('.') === -1) {
        this.append('.');
      }
    },
    setPrevious() {
      this.operatorClicked = true;
      this.previous = this.current;
    },
    divide() {
      this.operator = (a,b) => a / b;
      this.setPrevious();
    },
    multiply() {
      this.operator = (a,b) => a * b;
      this.setPrevious();
    },
    subtract() {
      this.operator = (a,b) => a - b;
      this.setPrevious();
    },
    add() {
      this.operator = (a,b) => a + b;
      this.setPrevious();
    },
    equal() {
      this.current = `${this.operator(
        parseFloat(this.previous), 
        parseFloat(this.current)
        )}`;
        this.previous = null;
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.calculator {
  width: 300px;
  margin: 0 auto;
  
  font-size: 30px;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
}
.display {
  text-align: end;
  padding: 2px 10px 0 0;
  grid-column: 1/5;
  background-color: slateblue;
}
.zero {
  grid-column: 1/3;
}
.btn {
  background-color: lightgrey;
  border: 1px solid #999;
}
.operator {
  background-color: orange;
  color: white;
}

</style>
