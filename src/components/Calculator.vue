<template>
  <div class="calculator">
    <div class="result">{{ current || '0'}}</div>
    <div @click="clear()" class="acBox">AC</div>
    <div @click="del()" class="elementBox">Del</div>
    <div @click="sign('/')" class="elementBox">/</div>
    <div @click="append('7')" class="elementBox">7</div>
    <div @click="append('8')" class="elementBox">8</div>
    <div @click="append('9')" class="elementBox">9</div>
    <div @click="sign('X')" class="elementBox">X</div>
    <div @click="append('6')" class="elementBox">6</div>
    <div @click="append('5')" class="elementBox">5</div>
    <div @click="append('4')" class="elementBox">4</div>
    <div @click="sign('-')" class="elementBox">-</div>
    <div @click="append('3')" class="elementBox">3</div>
    <div @click="append('2')" class="elementBox">2</div>
    <div @click="append('1')" class="elementBox">1</div>
    <div @click="sign('+')" class="elementBox">+</div>
    <div @click="append('0')" class="elementBox">0</div>
    <div @click="dot()" class="elementBox">.</div>
    <div @click="equal()" class="equalBox">=</div>
  </div>
</template>

<script>
export default {
  name: 'Calculator',
  data() {
    return {
      previous: null,
      current: '',
      operator: null,
      operatorClicked: false,
    }
  },
  methods: {
    clear() {
      this.current = '';
      this.previous = '';
    },
    del() {
      this.current = this.current.slice(0, -1);
    },
    sign(sign) {      
      switch(sign) {
        case '/':
          if (this.previous != null) {
            this.current = this.operator(parseFloat(this.previous),parseFloat(this.current));
            this.previous = null;
          }
          this.operator = (a,b) => a / b;
          this.setPrevious();
          break;
        case 'X':
          if (this.previous != null) {
            this.current = this.operator(parseFloat(this.previous),parseFloat(this.current));
            this.previous = null;
          }
          this.operator = (a,b) => a * b;
          this.setPrevious();
          break;
        case '-':
          if (this.previous != null) {
            this.current = this.operator(parseFloat(this.previous),parseFloat(this.current));
            this.previous = null;
          }
          this.operator = (a,b) => a - b;
          this.setPrevious();
          break;
        case '+':
          if (this.previous != null) {
            this.current = this.operator(parseFloat(this.previous),parseFloat(this.current));
            this.previous = null;
          }
          this.operator = (a,b) => a + b;
          this.setPrevious();
          break;
      }
    },
    append(number) {
      if (this.operatorClicked) {
        this.current = '';
        this.operatorClicked = false;
      }

      this.current = this.current + number;
    },
    dot() {
      if (this.current.indexOf('.') == -1) {
        this.append('.');
      }
    },
    setPrevious() {
      this.previous = this.current;
      this.operatorClicked = true;
    },
    equal() {
      this.current = this.operator(parseFloat(this.previous),parseFloat(this.current));
      this.previous = null;
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.calculator {
  margin-left: 200px;
  margin-right: 200px;
  font-size: 50px;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
}
.elementBox {
  background-color: gray;
  border: 1px solid black;
}
.acBox {
  grid-column: 1 / span 2;
  background-color: orange;
  color: white;
  border: 1px solid black;
}
.equalBox {
  grid-column: 3 / span 2;
  background-color: orange;
  color: white;
  border: 1px solid black;
}

.result {
  grid-column: 1 / 5;
  font-weight: bold;
  font-size: 100px;
}

</style>
