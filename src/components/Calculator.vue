<template>
  <div class="calculator">
  <div class="display ">
    <span class="displayCurent">{{current || 0}}</span>
    <span class="displayPrevious"></span>
  </div>
  <div @click="clear" class="btn">C</div>
  <div @click="sign" class="btn">+/-</div>
  <div @click="percent" class="btn">%</div>
  <div @click="divide" class="btn opp">/</div>  
  <div @click="append('7')" class="btn num">7</div>
  <div @click="append('8')" class="btn num">8</div>
  <div @click="append('9')" class="btn num">9</div>
  <div @click="multiply" class="btn opp">X</div>
  <div @click="append('4')" class="btn num">4</div>
  <div @click="append('5')" class="btn num">5</div>
  <div @click="append('6')" class="btn num">6</div>
  <div @click="minus" class="btn opp">-</div>
  <div @click="append('1')" class="btn num">1</div>
  <div @click="append('2')" class="btn num">2</div>
  <div @click="append('3')" class="btn num">3</div>
  <div @click="plus" class="btn opp">+</div>
  <div class="btn"></div>
  <div @click="append('0')" class="btn num">0</div>
  <div @click="dot()" class="btn">.</div>
  <div @click="equal" class="btn opp">=</div>
  </div>

</template>

<script>
export default {
 data(){
   return{
     current:'',
     operator:null,
     previous:null,
     operatorClicked:false
   }
 },
 methods:{
   clear(){
     this.current=''
   },
   sign(){
     this.current=this.current.charAt(0) === '-'?
       this.current.slice(1) : `-${this.current}`;
   },
   percent(){
     this.current = `${parseFloat(this.current) / 100}`;
   },
   append(number){
     if(this.operatorClicked){
       this.current ='';
       this.operatorClicked=false;
     }
     this.current= `${this.current}${number}`;
   },
   dot(){
     if(this.current.indexOf('.') === -1){
       this.append('.');
     }
   },
   setPrevious(){
     this.previous = this.current;
     this.operatorClicked = true;
   },
   divide(){
     this.operator=(a,b) => a / b;
     this.setPrevious()
     
   },
  minus(){
    this.operator =(a,b) => a - b;
    this.setPrevious()
    
  },
  plus(){
    this.operator = (a,b) => a + b;
    this.setPrevious()
    
  },
  multiply(){
    this.operator = (a,b) => a * b;
    this.setPrevious()
    
  },
  equal(){
    this.current = `${this.operator(
      parseFloat(this.current),
      parseFloat(this.previous)
    )}`;
    this.previous = null;
  }
 }

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.calculator{
  width:600px;
  margin: 0 auto;
  font-size: 40px;
  display: grid;
  grid-template-columns:repeat(4,1fr);
  background-color: #7F7E7E;
position: relative;
}
.display{
  grid-column: 1/5;
  height: 200px;
  background-color: #474747;
  color: #eee;
}
.zero{
  grid-column: 1/3;
}
.btn{
  background-color: #474747;
  border:1px solid #7F7E7E;
  cursor: pointer;
  color: #fff;
  transition: .2sl
}
.btn:hover{
background-color: #7F7E7E;
}
.num{
  background-color: #232323;
  color:#fff ;
}
.displayCurent{
  position: absolute;
  top: 120px;
  left: 50px;
}
</style>
