<template>
  <div class="program-result">
    <span>{{ stemWithIndex }}</span>
    <pre><code>{{ code }}</code></pre>

    <template v-for="(v, i) in input">
      <div class="small-problem" :key="i">
        <Row>
          <Col span="12" class="io-col">
            <span>{{ '(' + i + ') 输入' }}</span>
            <pre>{{ v }}</pre>
          </Col>
          <Col span="12" class="io-col">
            <span>{{ '(' + i + ') 输出' }}</span>
            <Input
              type="textarea"
              autosize
              width="50%"
              @on-blur="holdOutputChange"
              :element-id="String(i)"
            ></Input
          ></Col>
        </Row>
      </div>
    </template>
  </div>
</template>
<script>
export default {
  name: 'ProgramResult',
  props: {
    index: {
      type: Number,
      required: true
    },
    code: {
      type: String,
      required: true
    },
    input: {
      type: Array,
      required: true
    }
  },
  data() {
    return {
      output: []
    }
  },
  computed: {
    stemWithIndex() {
      return this.index
    }
  },
  methods: {
    holdOutputChange(event) {
      const src = event.srcElement
      this.$set(this.output, Number(src.id), src.value)
    }
  }
}
</script>
<style lang="less" scoped>
.io-col {
  padding: 5px 10px 5px 10px;
}
</style>


