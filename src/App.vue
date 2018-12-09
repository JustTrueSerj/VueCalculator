<template>
  <div id="app">
    <div id="calculator">
      <div class="result">{{ result }}</div>
    <div id="calcOperatorsLeft">
      <div @click="operation(operator)" v-for="operator in operatorsLeft" class="operatorLeft"> <p>{{ operator }}</p></div>
<div id="valOps">
  <div id="calcValues">
    <div @click="addResult(value)" class="values" v-for="value in values"> <p>{{ value }}</p></div>
  </div>
    <div id="calcOperatorsRight">
      <div @click="operation(operator)" v-for="operator in operatorsRight" class="operatorRight" > <p>{{ operator }}</p></div>
    </div>
    </div>
    </div>
    </div>
  </div>

</template>

<script>
export default {
  data () {
    return {
      colorOfValues: '',
      eqLast:false,
      eqBool:false,
      result:'0',
      values:[1,2,3,4,5,6,7,8,9,0, '1st Vue app by JTS'],
      operatorsLeft:['AC','C','%','+-','.',],
      operatorsRight:['+','-','*','/','^','='],
      arg1: undefined,
      arg2: undefined,
      operatorCalc:'',
      counterNext:false
    }
  },
  updated(){
  },
  methods:{
    addResult(value){
      if (value === '1st Vue app by JTS'){
        return alert('Первое приложение на Vue.js. :)  //Недоработано!')
      }
        if (Number(this.result) === (Number(this.arg1))){
          this.result=''
        }
      if (this.result==='0') this.result='';
     this.result += value},

    operation(operator){
      switch (operator) {
        case 'AC':
          return this.arg1=undefined, this.arg2=undefined, this.counterNext=false, this.eqBool=false, this.result='0';
          break;
        case 'C':
          if (this.result===this.arg1){
            return this.result='0', this.arg1=undefined}
            else{
               return this.result='0', this.arg2=undefined}
               break;
        case '+-':
          if( this.result.charAt(0) === '-' ){
            return this.result = this.result.slice(-(this.result.length-1))}else
              return this.result = '-'+this.result;
              break;
        case '.':
          for (let counter=0;counter<this.result.length-1;counter++){
          if ( this.result.charAt(counter) == '.'){
            return alert('Точка уже стоит')
          }}

          if (this.result.charAt(this.result.length-1) === '.'){
           return this.result = this.result.slice(0,-1)
          }
          else{
           return this.result = this.result+ '.'
          }
          break;
      }
      // if (operator === 'AC'){ return this.arg1=undefined, this.arg2=undefined, this.counterNext=false, this.result='0'  }
      // if (operator === 'C'){ if (this.result==this.arg1){ return this.result='0', this.arg1=undefined}else{
      //   return this.result='0', this.arg2=undefined
      // }}
      // if (operator === '+-'){ if(this.result.charAt(0) == '-'){return this.result = this.result.slice(-(this.result.length-1))}
      // else return this.result = '-'+this.result}

      if(this.arg1!==undefined && this.counterNext===true){
       if ((operator === '=') && this.eqBool){
         console.log(this.eqBool)

       }else{ this.arg2=this.result; this.eqBool=true}
        let arg1 = Number(this.arg1);
        let arg2 = Number(this.arg2);
        let res;
        console.log(arg1,arg2);
        switch (this.operatorCalc) {
          case '+':
            res = arg1 + arg2;
            break;
          case '-':
            res = arg1 - arg2;
            break;
          case '*':
            res = arg1 * arg2;
            break;
          case '/':
            if ( (arg1 == 0) || (arg2 == 0)){res='На 0 делить нельзя! Учи!'; break;}
            res = arg1 / arg2;
            break;
          case '^':
            res = Math.pow(arg1, arg2);
            break;
          case '%':
            res = arg1 % arg2;
            break;
        }
          let resultString = String(res);
          for (let counter = resultString.length - 1; counter > 0; counter--) {
            if (resultString.charAt(counter) == '.') {
              res = res.toFixed(counter)
            }
          }
        this.result = String(res);
        this.arg1=String(this.result);
        if (operator === '=') {
          this.arg2=String(arg2);
        }else{
          this.operatorCalc = operator;
        }
      }


        if (this.arg1==undefined){
          this.arg1=this.result;
          this.result='0';
          this.operatorCalc=operator;
          this.counterNext=true;
        }


      // case 'AC':
      //   this.arg1=0;
      //   this.arg2=0;
      //   this.operatorCalc=0;
      //   break;
      // case 'C':
      //   if (this.arg1!==''){
      //     this.arg2 = ''
      //   }else{
      //     this.arg1=''
      //   }
      //   break;
      //   default:
      //     alert( 'Ты что-то сломал)' );
      // }
    }
  }

}
</script>

<style lang="scss">
  #app{
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background:
      -webkit-linear-gradient(315deg, hsla(35, 95%, 55%, 1) 0%, hsla(35, 95%, 55%, 0) 70%),
      -webkit-linear-gradient(65deg, hsla(140, 90%, 50%, 1) 10%, hsla(140, 90%, 50%, 0) 80%),
      -webkit-linear-gradient(135deg, hsla(225, 95%, 50%, 1) 15%, hsla(225, 95%, 50%, 0) 80%),
      -webkit-linear-gradient(205deg, hsla(340, 100%, 55%, 1) 100%, hsla(340, 100%, 55%, 0) 70%);
    background:
      linear-gradient(135deg, hsla(35, 95%, 55%, 1) 0%, hsla(35, 95%, 55%, 0) 70%),
      linear-gradient(25deg, hsla(140, 90%, 50%, 1) 10%, hsla(140, 90%, 50%, 0) 80%),
      linear-gradient(315deg, hsla(225, 95%, 50%, 1) 15%, hsla(225, 95%, 50%, 0) 80%),
      linear-gradient(245deg, hsla(340, 100%, 55%, 1) 100%, hsla(340, 100%, 55%, 0) 70%);

  }
  #calculator{
    border: 3px solid lighten(gold,15%);
    border-radius: 10px;
    margin-top: 200px;
    margin-left: 550px;
    height: 353px;
    width: 350px;
  }
  @mixin buttons{
    display: inline-flex;
    border: 1px solid black;
    cursor: pointer;
    background-color: aqua;
    width: 50px;
    height: 50px;
    list-style: none;
    text-align: center;
    margin: 0.5px;
    border-radius: 10%;
    p{
      padding-left: 20px;
    }
  }
  .result{
    text-align: right;
    font-size:30px;
    background-color: red;
    width: 350px;
    height: 36px;
    border-radius: 8px;
   }
.values{
  @include buttons;
  border-radius: 15%;
  &:nth-child(10){
    width: 102px;
    padding-left: 54px;
  }
  &:last-child{
    background-color: gold;
    width: 102px;
    padding-left: 54px;
    p{
      margin-left: -57px;
      color: goldenrod;
    }
  }
  }
  .operatorRight{
    @include buttons;
    background-color: orange;
    width: 100px;
    font-size: 25px;
    p{
      margin-left: 23px;
      margin-top: 11px;

    }
    &:last-child{
      background-color: goldenrod;
      margin-left: -246px;
      width: 347px;
      p{
        margin-top: -9px;
        font-size: 50px;
        padding-left: 135px;
      }
    }
  }
  #calcValues{
    width: 160px;
    height: 220px;

}
  #calcOperatorsRight{
    margin-left: 159px;
    margin-top: -220px;
    width: 50px;
    height: 200px;
  }
#calcOperatorsLeft{
  height: 220px;
  width: 50px;
  margin-right: 1px;
}
  #valOps{
    margin-left: 88px;
    margin-top: -265px;
  }
  .operatorLeft{
    @include buttons;
    padding-right: 35px;
    background: gold;
    p{
      margin-left: 18px;
    }
    &:first-child{
      p{
        margin-left: 12px;}
    }
  }
</style>
