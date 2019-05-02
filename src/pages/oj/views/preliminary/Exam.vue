<template>
  <div>
    <Choice
      v-for="(v, i) in choices"
      :key="'choice-' + i"
      :index="i + choiceIndexOffest"
      :stem="v.stem"
      :options="v.options"
    ></Choice>
  </div>
</template>

<script>
import api from '@oj/api'
import Choice from './Choice'
export default {
  name: 'Exam',
  components: {
    Choice
  },
  data() {
    return {
      examID: 0,
      problems: {}
    }
  },
  mounted() {
    this.$Loading.start()
    this.examID = this.$route.params.examID
    api
      .getPreliminaryExam(this.examID)
      .then(res => {
        this.problems = res.data.problems
        this.$Loading.finish()
      })
      .catch(err => {
        console.log(err)
        this.$Loading.error()
      })
  },
  computed: {
    choices() {
      return this.problems.choice
    },
    choiceIndexOffest() {
      return 1
    }
  }
}
</script>
