<template>
  <div class="calculator">
    <div class="display">{{current || '0'}}</div>
    <div class='btn' @click="clear">C</div>
    <div class='btn' @click="sign">+/-</div>
    <div class='btn' @click="percent">%</div>
    <div class='btn operator' @click="divide">÷</div>
    <div class='btn' @click="append('7')">7</div>
    <div class='btn' @click="append('8')">8</div>
    <div class='btn' @click="append('9')">9</div>
    <div class='btn operator' @click="times">x</div>
    <div class='btn' @click="append('4')">4</div>
    <div class='btn' @click="append('5')">5</div>
    <div class='btn' @click="append('6')">6</div>
    <div class='btn operator' @click="minus">-</div>
    <div class='btn' @click="append('1')">1</div>
    <div class='btn' @click="append('2')">2</div>
    <div class='btn' @click="append('3')">3</div>
    <div class='btn operator' @click="plus">+</div>
    <div class="zero btn" @click="append('0')">0</div>
    <div class='btn' @click="dot">.</div>
    <div class='btn operator' @click='equal'>=</div>
  </div>
</template>

<script>
export default {
  name: 'Calculator',
  data(){
    return{
      current:'',
      previous:null,
      operatorClicked:false,
      operator: null
    }
  },
  methods:{
    clear(){
      this.current=''
    },
    sign(){
      this.current = this.current.charAt(0)==='-' ? this.current.slice(1) : `-${this.current}`
    },
    percent(){
      this.current=`${parseFloat(this.current)/100}`
    },
    append(number){
      if(this.operatorClicked){
        this.current =''
        this.operatorClicked=false
      }
      this.current=`${this.current}${number}`
    },
    dot(){
      if (this.current.indexOf('.') === -1){
        this.append('.')
      }
    },
    setPrevious(){
      this.previous = this.current
      this.operatorClicked = true
    },
    divide(){
      this.operator = (a,b)=>a/b
      this.setPrevious()
    },
    times(){
      this.operator = (a,b)=>a*b
      this.setPrevious()
    },
    minus(){
      this.operator = (a,b)=>a-b
      this.setPrevious()
    },
    plus(){
      this.operator = (a,b)=>a+b
      this.setPrevious()
    },
    equal(){
      this.current = `${this.operator(parseFloat(this.previous), parseFloat(this.current))}`
      this.previous = null;
    }
  }
  
}
</script>


<style scoped>
.calculator{
  display:grid;
  grid-template-columns: repeat(4,1fr);
  grid-auto-rows: minmax(50px, auto);
  font-size:40px;
  width:350px;
  margin:0 auto;
  grid-gap:5px;
  background:#444;
  padding:15px;
  border-radius:10px;
 
}
.display{
  grid-column:1/5;
  border:solid #999 1px;
   border-radius:10px;
   margin-bottom:10px;
   background:rgb(235, 235, 235);
}
.zero{
  grid-column:1/3;
}
.btn{
  background-color:#eee;
  
  border-radius:10px;
  cursor:pointer;
  transition: scale 0.2s linear;
  box-shadow: -5px -5px 2px #333
}
.operator{
  background-color: rgb(226, 74, 74);
  color:#fff;
}
.btn:active{
transform:scale(0.98)
}
</style>
