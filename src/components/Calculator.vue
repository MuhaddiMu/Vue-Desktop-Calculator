<template>
  <div class="Calc">
    <div class="Disp">{{Current || 0}}</div>
    <div @click="Clear" class="Btn">C</div>
    <div @click="ToggleAddSub" class="Btn">+/-</div>    
    <div @click="Percent" class="Btn">%</div>
    <div @click="Divide" class="Btn Operator">÷</div>
    <div @click="Append(7)" class="Btn">7</div>
    <div @click="Append(8)" class="Btn">8</div>    
    <div @click="Append(9)" class="Btn">9</div>
    <div @click="Times" class="Operator Btn">x</div>
    <div @click="Append(4)" class="Btn">4</div>
    <div @click="Append(5)" class="Btn">5</div>
    <div @click="Append(6)" class="Btn">6</div>
    <div @click="Minus" class="Operator Btn">-</div>
    <div @click="Append(3)" class="Btn">3</div>
    <div @click="Append(2)" class="Btn">2</div>
    <div @click="Append(1)" class="Btn">1</div>
    <div @click="Add" class="Operator Btn">+</div>
    <div @click="Append(0)" class="Btn Zero">0</div>
    <div @click="Period" class="Btn">.</div>
    <div @click="Equals" class="Operator Btn">=</div>

  </div>
</template>

<script>
export default {
  name: 'Calculator',
  props: {
    msg: String
  },
  data() {
    return {
      Previous: 'null',
      OperatorClicked: false,
      Current: '',
      Operator: null,
    }
  },
  methods: {
    Clear(){
      this.Current = ''

    },
    ToggleAddSub(){
      this.Current = this.Current.charAt(0) === '-' ? this.Current.slice(1) : `${this.Current*-1}`
    },
    Percent(){
      this.Current = `${parseFloat(this.Current)}`/100
    },
    Append(Val){
      if(this.OperatorClicked === true){
        this.Current = ''
        this.OperatorClicked = false
      }
      this.Current = `${this.Current}${Val}`
    },
    Period(){
      if(this.Current.indexOf('.') === -1 ){
        this.Append('.');
      }
    },
    SetPrevious(){
      this.Previous = this.Current
      this.OperatorClicked = true
    },
    Divide(){
      this.Operator = (A, B) =>  A/B
      this.SetPrevious()
    },

    Times(){
      this.Operator = (A, B) =>  A*B
      this.SetPrevious() 
    },

    Minus(){
      this.Operator = (A, B) =>  A-B
      this.SetPrevious()
    },

    Add(){
      this.Operator = (A, B) =>  A+B
      this.SetPrevious()
    },
    Equals(){
        this.Current = `${this.Operator(parseFloat(this.Previous), parseFloat(this.Current))}`
        this.Previous = null;
    },
   
  },
  created(){
    
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.Calc {
  width: 300px;
  margin: 0px auto;
  font-size: 40px;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto)
}

.Disp {
  color: white;
  background-color: #333;
  grid-column: 1/5;
}

.Zero {
  grid-column: 1/3;
}

.Btn {
  background-color: #f2f2f2;
  border: 1px solid #999;
  cursor: pointer;
}

.Btn:active{
  font-size: 35px
}

.Operator {
  background-color: orange;
  color: white;
}
</style>
