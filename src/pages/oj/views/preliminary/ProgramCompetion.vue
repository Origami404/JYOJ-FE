<template>
  <div ref="code"></div>
</template>
<script>
import Vue from 'vue'
export default {
  name: 'ProgramCompetion',
  props: {
    index: {
      type: Number,
      required: true
    },
    code: {
      type: String,
      required: true
    }
  },
  data() {
    return {
      answer: []
    }
  },
  mounted() {
    this.compile()
  },
  methods: {
    compile() {
      let result = ''
      let pos = 0
      while (pos < this.code.length) {
        if (this.code[pos] === '$') {
          pos += 1 // eat '$'
          let num = 0
          // Read a number after '$'
          while (
            '0'.charCodeAt() <= this.code[pos].charCodeAt() &&
            this.code[pos].charCodeAt() <= '9'.charCodeAt()
          ) {
            num += num * 10 + (this.code[pos].charCodeAt() - '0'.charCodeAt())
            pos += 1
          }
          // const Input = Vue.extend({
          //   template: `<i-input value="answer[${num}]"></i-input>`
          // })
          // const inputComponent = new Input().$mount()
          // this.$refs['input-' + num].appendChild(inputComponent.$el)
          // console.log(`Append: ${html}`)
          result += `<span><input></input></span>`
        } else {
          // console.log(`Append: ${this.code[pos]}`)
          const c = this.code[pos]
          if (c === '<') result += '&lt'
          else if (c === '>') result += '&gt'
          else if (c === '&') result += '&amp'
          else if (c === '"') result += '&quot'
          else result += c
          pos += 1
        }
      }
      const Code = Vue.extend({
        template: `<code><pre>${result}</pre></code>`
      })
      const codeComponent = new Code().$mount()
      this.$refs['code'].appendChild(codeComponent.$el)
      // return result
      console.log(result)
    }
  }
}
</script>
<style lang="less" scoped>
</style>

