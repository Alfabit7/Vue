<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <HelloWorld msg="Welcome to the calculator ;)"/>
    <input v-model.number="operand1"> <input v-model.number="operand2"> 
<h1>Результат {{operand1}} {{sign}} {{operand2}} равен {{result}}</h1>

<button @click='summation'>+</button>
<button @click='substraction' >-</button>
<button @click='didviding' v-if='(this.operand2!=0)'>\</button>
<button @click='multiplication'>*</button>
<button @click='exponentiation'>^</button>

  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  components: {
    HelloWorld
  },

   data(){
    return {
      operand1:'',
      operand2:'',
      result: '',
      sign:''
     }
   },
   methods:{
      summation(){
        this.result = this.operand1 + this.operand2;
        this.sign='+'
      },
      substraction(){
    this.result = this.operand1 - this.operand2;
    this.sign='-'
      },
      didviding(){
        this.result = this.operand1 / this.operand2;
        this.sign='/'
      },
      multiplication(){
 this.result = this.operand1 * this.operand2;
 this.sign='*'
      },
      exponentiation(){
      this.result = Math.pow(this.operand1, this.operand2)
      this.sign='^'
    },
   }

}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

button{
  margin: 10px 10px;
  width: 50px; height: 30px;
}
</style>
