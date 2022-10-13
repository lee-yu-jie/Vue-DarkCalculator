<template>
  <main>
    <div class="calc">
      <div class="display">{{display}}</div>
      <div class="row">
        <button @click="clear" class="special-key">AC</button>
        <button @click="concatNum('1')" class="special-key">+/-</button>
        <button class="special-key">&#37;</button>
        <button class="operator-key">&#247;</button>
      </div>
      <div class="row">
        <button @click="concatNum('7')" class="number-key">7</button>
        <button @click="concatNum('8')" class="number-key">8</button>
        <button @click="concatNum('9')" class="number-key">9</button>
        <button class="operator-key">&#215;</button>
      </div>
      <div class="row">
        <button @click="concatNum('4')" class="number-key">4</button>
        <button @click="concatNum('5')" class="number-key">5</button>
        <button @click="concatNum('6')" class="number-key">6</button>
        <button class="operator-key">–</button>
      </div>
      <div class="row">
        <button @click="concatNum('1')" class="number-key">1</button>
        <button @click="concatNum('2')" class="number-key">2</button>
        <button @click="concatNum('3')" class="number-key">3</button>
        <button class="operator-key">+</button>
      </div>
      <div class="row">
        <button @click="concatNum('0')" class="number-key double-size">0</button>
        <button @click="addPoint('.')" class="number-key">.</button>
        <button class="operator-key">=</button>
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
        display.value === 0 ? display.value = num : display.value += num
      }
      const clear = () => {
        display.value = '0'
      }
      const addPoint = (point) => {
        if(display.value.indexOf('.') === -1){
          display.value += point
        }
      }




    return{ 
      display,
      concatNum,
      clear,
      addPoint
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
  box-shadow: 0 0 100px rgb(78, 78, 78);
  .display{
    text-align: end;
    margin-bottom: 1em;
    padding: .5em 1em;
    border: rgb(29, 29, 29) 4px solid;
    border-radius: 2em;
    background: $bgColor;
    box-shadow: $shadow, $inside-shadow;
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
    button[class*='double-size']{
      width: 140px;
      border-radius: 2em;
    }
    button:hover{
      color: $ft-color;
      box-shadow: $inside-shadow;
    }
  }
}


</style>
