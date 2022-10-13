<template>
  <main>
    <div class="calc">
      <div class="display">{{display}}</div>
      <div class="row">
        <button @click="clear" class="special-key">AC</button>
        <button @click="negative" class="special-key">+/-</button>
        <button @click="percent" class="special-key">%</button>
        <button @click="concatOp('/')" class="operator-key">÷</button>
      </div>
      <div class="row">
        <button @click="concatNum('7')" class="number-key">7</button>
        <button @click="concatNum('8')" class="number-key">8</button>
        <button @click="concatNum('9')" class="number-key">9</button>
        <button @click="concatOp('*')" class="operator-key">×</button>
      </div>
      <div class="row">
        <button @click="concatNum('4')" class="number-key">4</button>
        <button @click="concatNum('5')" class="number-key">5</button>
        <button @click="concatNum('6')" class="number-key">6</button>
        <button @click="concatOp('-')" class="operator-key">–</button>
      </div>
      <div class="row">
        <button @click="concatNum('1')" class="number-key">1</button>
        <button @click="concatNum('2')" class="number-key">2</button>
        <button @click="concatNum('3')" class="number-key">3</button>
        <button @click="concatOp('+')" class="operator-key">+</button>
      </div>
      <div class="row">
        <button @click="concatNum('0')" class="number-key">0</button>
        <button @click="dele" class="number-key">></button>
        <button @click="addPoint('.')" class="number-key">.</button>
        <button @click="evaluate" class="operator-key">=</button>
      </div>
    </div>
  </main>  
</template>

<script>
import { ref } from 'vue'
export default {
    setup() {
      const display = ref('0')
      const concatNum = (num) => {
        display.value === '0' ? display.value = num : display.value += num
      }
      const concatOp = (op) => {
        display.value.search(/\D$/) === -1 && (display.value += op)
      }
      const clear = () => {
        display.value = '0'
      }
      const dele = () => {
        display.value = display.value.substring(0, display.value.length - 1)
        display.value === '' && (display.value = '0')
      }
      const negative = () => {
        if( display.value !== '0' && display.value.indexOf('-') === -1){
          display.value = '-' + display.value
        }else if(display.value.indexOf('-') !== -1){
          display.value = display.value.replace('-','')
        }
      }
      const percent = () => {
        if(display.value.search(/\D/) === -1 || display.value.indexOf('.') !== -1){
          display.value = String(display.value / 100)
        }
      }
      const addPoint = (point) => {
        if(display.value.indexOf('.') === -1 && display.value.search(/\D$/) === -1){ 
          (display.value += point)
        }
      }
      const evaluate = () => {
        display.value = String(eval(display.value))
      }

    return{ 
      display,
      concatNum,
      clear,
      addPoint,
      concatOp,
      dele,
      negative,
      percent,
      evaluate
    }
  }
}
</script>
<style lang="scss">
$shadow:  -5px -5px 10px rgb(41, 41, 41),
          5px 5px 10px black;
$inside-shadow: 5px 5px 10px black inset,
            -5px -5px 10px rgb(41, 41, 41) inset;
$bgColor: rgb(22, 22, 22);
$border: rgb(29, 29, 29) 1px solid;
$ft-color: rgb(31, 157, 155);
body{
  background: black;
}
main{
  padding-top: 5em;
}
.calc{
  color: $ft-color;
  font-size: 1.5em;
  animation: shadow 5s linear infinite;
  .display{
    text-align: end;
    margin-bottom: 1em;
    padding: .5em 1em;
    border: rgb(29, 29, 29) 4px solid;
    border-radius: 2em;
    background: $bgColor;
    box-shadow: $shadow, $inside-shadow;
    word-break: break-all;
  }
  width: 300px;
  background: $bgColor;
  margin: 0 auto;
  padding: 2em;
  border-radius: 2em;
  .row{
    display: flex;
    justify-content: space-between;
    button{
      width: 60px;
      height: 60px;
      margin-bottom: 1em;
      border: $border;
      border-radius: 100%;
      color: white;
      background: $bgColor;
      box-shadow: $shadow;
      font-size: 1em;
      cursor: pointer;
    }
    button:hover{
      color: $ft-color;
      box-shadow: $inside-shadow;
    }
  }
  @keyframes shadow {
    0%{box-shadow: 0 0 100px rgb(78, 78, 78)}
    33%{box-shadow: 0 0 50px rgb(78, 78, 78)}
    66%{box-shadow: 0 0 110px rgb(111, 110, 110)}
    100%{box-shadow: 0 0 90px rgb(78, 78, 78)}
  }
}


</style>
