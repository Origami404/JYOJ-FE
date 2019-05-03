<template>
  <div>
    <panel shadow id="exam">
      <div slot="title" class="exam-title">{{ examName }}</div>
      <div class="problems">
        <div class="choice-panel">
          <p class="big-problem-title">一. 单选题</p>
          <Choice
            v-for="(v, i) in problems.choice"
            :key="'choice-' + i"
            :index="i + choiceIndexOffest"
            :stem="v.stem"
            :options="v.options"
            ref="choice"
            class="question"
          ></Choice>
        </div>
        <div class="multichoice-panel">
          <p class="big-problem-title">二. 多选题</p>
          <Multichoice
            v-for="(v, i) in problems.multichoice"
            :key="'multichoice-' + i"
            :index="i + multichoiceIndexOffset"
            :stem="v.stem"
            :options="v.options"
            ref="multichoice"
            class="question"
          ></Multichoice>
        </div>
        <div class="gap-filling-panel">
          <p class="big-problem-title">三. 填空题</p>
          <GapFilling
            v-for="(v, i) in problems.gap_filling"
            :key="'gap-filling-' + i"
            :index="i + gapFillingIndexOffset"
            :stem="v.stem"
            ref="gapFilling"
            class="question"
          ></GapFilling>
        </div>

        <div class="program-result">
          <p class="big-problem-title">四. 看程序写结果</p>
          <ProgramResult
            v-for="(v, i) in problems.program_result"
            :key="'program-result-' + i"
            :index="i + programResultIndexOffset"
            :code="v.code"
            :input="v.input"
            ref="programResult"
            class="question"
          ></ProgramResult>
        </div>
      </div>

      <Button @click="sublime"> Sublime </Button>
    </panel>
  </div>
</template>

<script>
import api from '@oj/api'
import Choice from './Choice'
import Multichoice from './Multichoice'
import GapFilling from './GapFilling'
import ProgramResult from './ProgramResult'
export default {
  name: 'Exam',
  components: {
    Choice,
    Multichoice,
    GapFilling,
    ProgramResult
  },
  data() {
    return {
      examID: 0,
      examName: '',
      problems: {}
    }
  },
  mounted() {
    this.$Loading.start()
    this.examID = this.$route.params.examID
    api
      .getPreliminaryExam(this.examID)
      .then(res => {
        this.examName = res.data.name
        this.problems = res.data.problems
        this.$Loading.finish()
      })
      .catch(err => {
        console.log(err)
        this.$Loading.error()
      })
  },
  computed: {
    choiceIndexOffest() {
      return 1
    },
    multichoiceIndexOffset() {
      return this.choiceIndexOffest + this.problems.choice.length
    },
    gapFillingIndexOffset() {
      return this.multichoiceIndexOffset + this.problems.multichoice.length
    },
    programResultIndexOffset() {
      console.log(this.problems.program_result)
      return this.gapFillingIndexOffset + this.problems.gap_filling.length
    }
  },
  methods: {
    sublime() {
      let answer = {
        answer: {
          choice: this.$refs.choice.map(item => item.choosenOptionIndex),
          multichoice: this.$refs.multichoice.map(item => item.choosenOptions),
          gap_filling: this.$refs.gapFilling.map(item => item.answer),
          program_result: this.$refs.programResult.map(item => item.output)
        }
      }
      console.log(answer)
    }
  }
}
</script>
<style lang="less" scoped>
.problems {
  padding: 0px 30px 10px 30px;
}
.exam-title {
  font-size: 21px;
  font-style: italic;
}
.big-problem-title {
  font-size: 15px;
  font-weight: bold;
  padding: 1px 0px 1px 0px;
}
.question {
  padding-left: 5px;
}
</style>

