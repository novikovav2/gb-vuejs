<template>
  <div class="hello">
    <input v-model.number="operand1"/>
    <input v-model.number="operand2"/>
    = {{ result }}
    <br>
    <button @click="calculate('sum')">+</button>
    <button @click="calculate('sub')">-</button>
    <button @click="calculate('mul')">*</button>
    <button @click="calculate('div')">/</button>
    <button @click="calculate('pow')">^</button>
    <button @click="calculate('div2')">%</button>

    <br>
    <input type="checkbox"  v-model="showKeyboard"> Показать клавиатуру
    <div v-if="showKeyboard">
      <button v-for="num in 10"
              :key="num-1"
              @click="insertNumber(num - 1)">
        {{ num - 1 }}
      </button>
      <button @click="clear">
        Clear
      </button>
      <br>
      <input type="radio" id="one" value="1" v-model="picked">
      <label for="one">Операнд 1</label>
      <input type="radio" id="two" value="2" v-model="picked">
      <label for="two">Операнд 2</label>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data: () => ({
    operand1: 0,
    operand2: 0,
    result: 0,
    showKeyboard: true,
    picked: '1'
  }),
  props: {
  },
  methods: {
    calculate (operation) {
      switch (operation) {
        case 'sum':
          this.result = this.operand1 + this.operand2
          break
        case 'sub':
          this.result = this.operand1 - this.operand2
          break
        case 'mul':
          this.result = this.operand1 * this.operand2
          break
        case 'div':
          this.result = this.operand1 / this.operand2
          break
        case 'div2':
          this.result = (this.operand1 - this.operand1 % this.operand2) / this.operand2
          break
        case 'pow':
          this.result = this.operand1 ** this.operand2
          break
      }
    },
    insertNumber (num) {
      this.picked === '1' ? this.operand1 = this.operand1 * 10 + num : this.operand2 = this.operand2 * 10 + num
    },
    clear () {
      if (this.picked === '1') {
        this.operand1 = (this.operand1 - this.operand1 % 10) / 10
      } else {
        this.operand2 = (this.operand2 - this.operand2 % 10) / 10
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
