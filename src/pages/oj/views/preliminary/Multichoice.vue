<template>
  <div class="multichoice">
    <p>{{ stemWithIndex }}</p>
    <CheckboxGroup v-model="choosenOptions" vertical class="checkbox-group">
      <Checkbox
        v-for="(v, i) in options"
        :key="i"
        :label="i"
        class="checkbox"
        >{{ optionIndexToAlpha(i) + '. ' + v }}</Checkbox
      >
    </CheckboxGroup>
  </div>
</template>
<script>
export default {
  name: 'Multichoice',
  props: {
    index: {
      type: Number,
      required: true
    },
    stem: {
      type: String,
      required: true
    },
    options: {
      type: Array,
      required: true
    }
  },
  data() {
    return {
      choosenOptions: []
    }
  },
  computed: {
    stemWithIndex() {
      return this.index + '. ' + this.stem
    }
  },
  methods: {
    optionIndexToAlpha(index) {
      return String.fromCharCode(index + 'A'.charCodeAt(0))
    }
  }
}
</script>

<style lang="less" scoped>
.checkbox-group {
  padding-left: 7px;
}
</style>
