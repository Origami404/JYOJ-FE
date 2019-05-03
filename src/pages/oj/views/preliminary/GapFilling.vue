<template>
  <div>
    <p>{{ index + '. ' + stem }}</p>
    <Input v-model="answer" class="input-box"></Input>
  </div>
</template>
<script>
export default {
  name: 'GapFilling',
  props: {
    index: {
      type: Number,
      required: true
    },
    stem: {
      type: String,
      required: true
    }
  },
  data() {
    return {
      answer: ''
    }
  }
}
</script>
<style lang="less" scoped>
.input-box {
  width: 50%;
}
</style>
