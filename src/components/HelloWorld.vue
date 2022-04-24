<template>
  <div class="hello">
    <input v-model.number="operand1" >
    <input v-model.number="operand2" >
    ={{result}}
    <div>
      <button v-for="(op,index) in operations" @click = "calculate( op )" v-bind:key="index">
        {{op}}
      </button>
    </div>
    <label >
      <input :class="[$style.title]"  type="checkbox" v-model="showvk" >
         Отобразить экранную клавиатуру
      </label>
    <div v-if="showvk" >
      <div>
         <button :class="[$style.btn]" v-for="btn in 10" :key="btn" @click="inputNum(btn -1)">
            {{btn - 1}}
          </button>
          <button @click="eraseOne" >&larr;</button>
      </div>
      <label class="radio"><input type="radio" value="1" v-model="operCh" > Операнд1 </label>
      <label><input type="radio" value="2" v-model="operCh" > Операнд2 </label>
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
    operations: ['+', '-', '/', '*'],
    showvk: false,
    arrow: '&larr',
    operCh: ''
  }),
  props: {
  },
  methods: {
    inputNum (i) {
      const { operCh } = this
      const input = operCh === '1' ? 'operand1' : 'operand2'
      this[input] = +(this[input] += String(i))
    },
    eraseOne () {
      const { operCh } = this
      const input = operCh === '1' ? 'operand1' : 'operand2'
      this[input] = Math.trunc(this[input] / 10)
    },
    calculate (op) {
      const { operand1, operand2 } = this

      const calcOp = {
        '+': () => operand1 + operand2,
        '-': () => operand1 - operand2,
        '/': () => operand1 / operand2,
        '*': () => operand1 * operand2
      }
      this.result = calcOp[op]()
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss" module>
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
.error {
  padding: 2px;
  border: 1px solid red;
}
.btn {
  margin: 10px 0;
}
.title {
  margin-top: 10px;
}
</style>
