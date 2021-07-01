<template>
<div>
  <h1>{{ title }}</h1>
    <div>
        <input type="number" placeholder="op1" v-model.number="operand1">
        <input type="number" placeholder="op2" v-model.number="operand2">
        = {{ result }}
    </div>
      <div>
        <button @click="add">+</button>
        <button v-on:click="substract">-</button>
        <button @click="multiply">*</button>
        <button @click="divide">/</button>
        <button v-on:click="expo">^</button>
        <button v-on:click="int">%</button>
        <button @click="eventFn">Event</button>
      </div>
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
    title: 'Калькулятор'
  }),
  methods: {
    add () {
      this.result = this.operand1 + this.operand2
    },
    substract () {
      this.result = this.operand1 - this.operand2
    },
    divide () {
      this.result = this.operand1 / this.operand2
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
    }
  }
}

</script>
