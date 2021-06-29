<template>
<div>
  <h1>{{ title }}</h1>
    <div>
        <input type="number" placeholder="op1" v-model.number="operand1">
        <input type="number" placeholder="op2" v-model.number="operand2">
        = {{ sum }}
    </div>
      <div>
        <button @click="sum = operand1 + operand2">+</button>
        <button v-on:click="sum = operand1 - operand2">-</button>
        <button @click="sum = operand1 * operand2">*</button>
        <button @click="div">/</button>
        <button v-on:click="expo">^</button>
        <button v-on:click="int">%</button>
        <button @click="eventFn">Event</button>
      </div>
    Result {{ sum }}
</div>
</template>

<script>

export default {
  name: 'Calc',
  data: () => ({
    operand1: 0,
    operand2: 0,
    sum: 0,
    title: 'Калькулятор'
  }),
  methods: {
    eventFn () {
      console.log(arguments)
    },
    div () {
      this.sum = this.operand1 / this.operand2
    },
    expo () {
      this.sum = Math.pow(this.operand1, this.operand2)
    },
    int () {
      if (this.operand1 < this.operand2) {
        this.sum = Math.floor(this.operand1 / this.operand2)
      } else if (this.operand1 > this.operand2) {
        this.sum = Math.ceil(this.operand1 / this.operand2)
      }
    }
  }
}

</script>
