<template>
  <div class="p-3" style="max-width: 400px; margin: 50px auto; background: #234;">
    <div class="w-full rounded m-1 p-3 text-right lead font-weight-bold text-white bg-vue-dark">
      {{ calculatorValue || 0 }}
      </div>
    <div class="row no-gutters">
      <div class="col-3" v-for="e in calculatorElements" :key="e">
      <div
      class="lead text-center text-white m-1 py-3 bg-vue-dark rounded hover-class"
      :class="{'bg-vue-green' : ['C','*','/','-','+','%','='].includes(e)}" 
      @click="action(e)"> <!-- includes() FIND the returns true if a string contains a specified string FIND. -->
      {{e}}
      </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Calculator-App",
  data() {
    return {
      calculatorValue: '',
      calculatorElements: ['C','*','/','-',7,8,9,'+',4,5,6,'%',1,2,3,'=',0,'.'],
      prevCalculatorValue: null,
      operator: null
    }
  },
  methods: {
    action (e) {
      if (!isNaN(e) || e === '.') {
        this.calculatorValue += e + ''
      }
      if (e === 'C') {
        this.calculatorValue = ''
      }
      if (['/','*','+','-'].includes(e)) {
        this.operator = e
        this.prevCalculatorValue = this.calculatorValue
        this.calculatorValue = ''
      }
      if (e === '%') {
        this.calculatorValue = this.calculatorValue / 100 + ''
      }
      if (e === '=') {
        this.calculatorValue = eval(
          this.prevCalculatorValue + this.operator + this.calculatorValue
        )
        this.prevCalculatorValue = null
        this.operator = null
      }

    }
  }
}
</script>

<style scoped>
.bg-vue-dark {
  background: #31475e;
  text-align: right;
}
.hover-class:hover {
  cursor: pointer;
  background: #3D5875;
}
.bg-vue-green {
  background: #3fb984;
}

</style>
