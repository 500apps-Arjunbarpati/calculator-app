<template>
<h1> Calculator</h1>
  <div class="calculator">
  <div class="dispaly">{{current || '0'}}</div>
  <div @click="clear" class ="button">clear</div>
  <div @click="sign" class ="button">+/-</div>
<div @click="percent" class ="button">%</div>
<div @click="divide" class ="button operator">/</div>
<div @click="append('7')" class ="button">7</div>
<div @click="append('8')" class ="button">8</div>
<div @click="append('9')" class ="button">9</div>
<div @click="multiply" class ="button operator">*</div>
<div @click="append('4')" class ="button">4</div>
<div @click="append('5')" class ="button">5</div>
<div @click="append('6')" class ="button">6</div>
<div @click="minus" class ="button operator">-</div>
<div @click="append('1')" class ="button">1</div>
<div @click="append('2')" class ="button">2</div>
<div @click="append('3')" class ="button">3</div>
<div @click="add" class ="button operator">+</div>
<div @click="append('0')" class="button zero">0</div>
<div @click="dot" class ="button">.</div>
<div @click="equal" class ="button operator">=</div>


  </div>
</template>

<script>
export default {
  data(){
    return{
      current:'500',
      operator:null,
      previous:null,
      operatorClicked:false, 
    }
  },
  methods:{
    clear(){
      this.current='';
  },
  sign(){
    this.current=this.current.charAt(0)==='-'?
    this.current.slice(1):`-${this.current}`;
  },
  percent(){
    this.current=`${parseFloat(this.current) /100 }`;
  },
  append(number){
    if(this.operatorClicked){
      this.current='';
      this.operatorClicked=false;
    }
this.current= `${this.current}${number}`;
  
  },
  dot(){
    if(this.current.indexOf('.')===-1){
      this.append('.')
    }
  },
  setPrevious(){
this.previous=this.current;
this.operatorClicked=true;
  },
  divide(){
this.operator=(a,b) => b/a;
this.setPrevious();
  },
  multiply(){
this.operator=(a,b)=>a*b;
 this.setPrevious();
 },
  minus(){
this.operator=(a,b)=>b-a;
this.setPrevious();
  },
  add(){
this.operator=(a,b)=>a+b;
this.setPrevious();
  },
  equal(){
this.current = this.operator(
         parseFloat(this.current), 
        parseFloat (this.previous)
          );
   this.previous=null;
  }
}}
</script>


<style scoped>
.calculator{
  margin: 0 auto;
  width:400px;
  text-align: center;
  display: grid;
  font-size: 40px;
 grid-template-columns:repeat(4,1fr);
 grid-auto-rows: (50px,auto);
}
.dispaly{
    grid-column: 1/5;
    background-color:black;
    color:white;
  }
  .button{
    background-color: darkgray;
    border:1px solid #999;
  }
  .zero{
    grid-column: 1/3;
  }
  .operator
  {
    background-color: orange;
  color:white;
  }
  h1{
    text-align: center;
  }

</style>
