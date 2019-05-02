<template>
  <div>
    <p>{{ stemWithIndex }}</p>
    <Radio-group :model.sync="choosenOptionIndex">
      <Radio v-for="(v, i) in options" :key="i" :value="i">
        {{ optionIndexToAlpha(i) + '. ' + v }}
      </Radio>
    </Radio-group>
  </div>
</template>
<script>
export default {
  name: 'Choice',
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
      choosenOptionIndex: ''
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
