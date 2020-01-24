<template>
  <div class=calculator>
    <div class="display">{{ currentValue || ''}}</div>
    <div @click="clear" class="btn">C</div>
    <div @click="switchSign" class="btn">+/-</div>
    <div @click="percentage" class="btn">%</div>
    <div @click="divide" class="btn operator">÷</div>
    <div @click ="append('7')" class="btn">7</div>
    <div @click ="append('8')" class="btn">8</div>
    <div @click ="append('9')" class="btn">9</div>
    <div @click="times" class="btn operator">x</div>
    <div @click ="append('4')" class="btn">4</div>
    <div @click ="append('5')" class="btn">5</div>
    <div @click ="append('6')" class="btn">6</div>
    <div @click="add" class="btn operator">+</div>
    <div @click ="append('1')" class="btn">1</div>
    <div @click ="append('2')" class="btn">2</div>
    <div @click ="append('3')" class="btn">3</div>
    <div @click="minus" class="btn operator">-</div>
    <div @click ="append('0')" class="btn zero">0</div>
    <div @click="dot" class="btn">.</div>
    <div @click="equal" class="btn operator">=</div>


  </div>
</template>

<script>
  export default {
    data(){
      return{
        currentValue: '',
        previousValue:'',
        operator:null,
        operatorClicked: false
      }
    },
    methods: {
      clear(){
        this.currentValue = ''
      },
      switchSign(){
        if(this.currentValue.charAt(0)==='-'){
          this.currentValue = this.currentValue.slice(1)
        }else{
          this.currentValue = `-${this.currentValue}`
        }
      },
      percentage(){
        this.currentValue = this.currentValue * 0.01
      },
      append(number){
        if(this.operatorClicked){
          this.currentValue = ''
          this.operatorClicked = false
        }
        this.currentValue = `${this.currentValue}${number}`
      },
      setPrevious(){
        this.previousValue = this.currentValue
        this.operatorClicked = true
      },
      divide(){
        this.operator = (a,b)=> a / b
        this.setPrevious()
      },
      times(){
        this.operator = (a,b)=> a * b
        this.setPrevious()
      },
      add(){
        this.operator = (a,b) => a + b
        this.setPrevious()
      },
      minus(){
        this.operator = (a,b) => a - b
        this.setPrevious()
      },
      dot(){
        if(this.currentValue.indexOf('.')=== -1){
          this.append('.')
        }
      },
      equal(){
        this.currentValue = `${this.operator(
          parseFloat(this.previousValue),
          parseFloat(this.currentValue)
        )}`
        this.previousValue = null
      }
    }
  }
</script>

<style scoped>
  .calculator {
    margin: 0 auto;
    width: 700px;
    font-size: 50px;
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    grid-auto-rows: minmax(100px, auto);
  }
  .display {
    grid-column: 1 / 5;
    background-color: #d55262;
    color: white;
  }
  .zero {
    grid-column: 1 / 3;
  }
  .btn {
    background-color: #56696b;
    border: 1px solid #999;
  }
  .operator {
    background-color: rgba(19, 19, 49, 0.79);
    color: white;
  }
</style>
