<template>
<div>
  <h1>{{ title }}</h1>
    <div>
        <input type="number" placeholder="op1" v-model.number="operand1">
        <input type="number" placeholder="op2" v-model.number="operand2">
        = {{ result }} - {{ fibResult}}
    </div>
    <div class="error" v-if="error">Ошибка: {{ error }}</div>
     <div class="strang-message">
         <template v-if="result < 0">Отрицательное число</template>
         <template v-else-if="result < 100">Число меньше 100</template>
         <template v-else>Число больше 100</template>
     </div>
     <div class="clollection">
       <div v-for="(item, idx) in collection" :key="idx">
        {{ idx + 1 }} - {{ item }}
       </div>
     </div>
     <div class="buttons">
         <button v-for="btn in buttons"
         :key="btn"
         v-bind:title="btn"
         :disabled="operand2 === 0"
         @click="calculate(btn)">
         {{ btn }}</button>
     </div>
     <div class="logs">
       {{ logs }}
     </div>
    <!--       <div>
        <button @click="calculate('+')">+</button>
        <button @click="calculate('-')">-</button>
        <button @click="calculate('*')">*</button>
        <button @click="calculate('/')">/</button>
        <button @click="calculate('^')">^</button>
        <button @click="calculate('%')">%</button>
      </div> -->
    Result {{ result }}
</div>
</template>

<script>

export default {
  name: 'Calc',
  data: () => ({
    operand1: 0,
    operand2: 0,
    result: 0,
    title: 'Калькулятор',
    buttons: ['+', '-', '*', '/', '^', '%'],
    collection: [1, 2, 3, 4, 5, 6, 7, 8, 9, 0],
    fibResult: 0,
    logs: {},
    error: ''
  }),
  methods: {
    fib (n) {
      return n <= 1 ? n : this.fib(n - 1) + this.fib(n - 2)
    },
    calculate (operation = '+') {
      this.error = ''
      switch (operation) {
        case '+':
          this.add()
          break
        case '-':
          this.substract()
          break
        case '*':
          this.multiply()
          break
        case '/':
          this.divide()
          break
        case '^':
          this.expo()
          break
        case '%':
          this.int()
          break
      }
      const key = Date.now()
      const value = `${this.operand1} ${operation} ${this.operand2} = ${this.result}`
      this.$set(this.logs, key, value)
    },
    /*     calculate (op) {
      const calcOperations = {
        '+': () => this.operand1 + this.operand2,
        '-': () => this.operand1 - this.operand2,
        '*': () => this.operand1 * this.operand2,
        '/': () => this.operand1 / this.operand2,
        '^': () => Math.pow(this.operand1, this.operand2),
        '%': () => Math.ceil(this.operand1 / this.operand2)
      }
      this.result = calcOperations[op]()
    }, */
    add () {
      this.result = this.operand1 + this.operand2
      // this.fibResult = this.fib(this.operand1) + this.fib(this.operand2)
      this.fibResult = this.fib1 + this.fib2
    },
    substract () {
      this.result = this.operand1 - this.operand2
      this.fibResult = this.fib1 - this.fib2
    },
    divide () {
      const { operand1, operand2 } = this
      if (operand2 === 0) {
        this.error = 'На ноль делить нельзя'
      } else {
        this.result = operand1 / this.operand2
      }
    },
    multiply () {
      this.result = this.operand1 * this.operand2
    },
    expo () {
      this.result = Math.pow(this.operand1, this.operand2)
    },
    int () {
      if (this.operand1 < this.operand2) {
        this.result = Math.floor(this.operand1 / this.operand2)
      } else if (this.operand1 > this.operand2) {
        this.result = Math.ceil(this.operand1 / this.operand2)
      }
    },
    computed: {
      fib1 () {
        return this.fib(this.operand1)
      },
      fib2 () {
        return this.fib(this.operand2)
      }
    }
  }
}

</script>

<style scoped>
.error {
  color: red
}
</style>
