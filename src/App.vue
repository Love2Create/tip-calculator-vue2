<template>
  <div id="app">
    <!-- <img alt="Vue logo" src="./assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/> -->

    <main id="calculator-container" @input="inputChange">
      <h1>Tip Calculator</h1>
      <section>
        <div>
          <div class="billInput">
            <label for="bill">Bill Total</label>
            <input type="Number" id="bill" placeholder="enter your bill total" v-model="billEntered">
          </div>
          <div class="space-between">
            <label for="tipPercent">Tip Percentage</label>
            <span>{{tipPercentSliderStr + "%"}}</span>
          </div>
            <input
            type="range" 
            min="0" 
            max="100"
            id="tipPercent" 
            placeholder="enter your bill total"
            v-model="tipPercentSliderStr">
          <div class="space-between" >
            <span>Tip</span>
            <span>{{ "$" + tipAmount }}</span>
          </div>
          <hr>
          <div class="space-between">
            <span>Total</span>
            <span>{{ "$" + billTotal }}</span>
          </div>
        </div>
      </section>
      <section>
        <div class="space-between">
           <span>Split</span>
           <span>{{ splitByNum > 1 ? splitByNum +" people" : "1 person" }}</span>
        </div>
            <input type="range" min="1" max="10" value="1" id="splitBy" v-model="splitByNum">
        <div class="space-between">
            <span>Bill Each</span>
            <span>{{ "$" + billEach }}</span>
        </div>
        <div class="space-between">
            <span>Tip Each</span>
            <span>{{ "$" + tipEach }}</span>
        </div>
        <div class="space-between">
            <span>Total Per Person with tip</span>
            <span>{{ "$" + totalPerPersonWithTip }}</span>
        </div>
      </section>
    </main>

  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  data(){
    return{
      billEntered: "",
      tipPercentSliderStr: 0,
      tipAmount: 0,
      billTotal: 0,
      splitByNum: 1,
      billEach: 0,
      tipEach: 0,
      totalPerPersonWithTip: 0,
    }
  },
  methods:{
    inputChange(){
      this.tipAmount = this.billEntered * (Math.ceil(Number(this.tipPercentSliderStr))/100);
      this.tipAmount = this.tipAmount.toFixed(2);
      this.billTotal = Number(this.billEntered) + Number(this.tipAmount);
      this.billEach = Number(this.billEntered)/Number(this.splitByNum);
      this.billEach = Math.ceil((this.billEach)*100)/100;
      this.tipEach = this.tipAmount/Number(this.splitByNum);
      this.tipEach = Math.ceil(Number(this.tipEach)*100)/100;
      this.totalPerPersonWithTip = this.billEach + this.tipEach;
      this.totalPerPersonWithTip = (this.totalPerPersonWithTip*100)/100;
    },
  },
}
</script>

<style lang="scss">
@import "./style.scss";
@import url('https://fonts.googleapis.com/css2?family=Lato&family=Mochiy+Pop+P+One&display=swap');
</style>
