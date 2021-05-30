<template>
  <div class="questions-ctr">
      <div class="progress">
        <div class="bar" :style="{ width: `${questionsAwnsered / questions.length * 100}%`}"></div>
        <div class="status">{{ questionsAwnsered }} out of {{ questions.length }} questions awnsered</div>
      </div>
      <transition-group name="fade">
          <div class="single-question" v-for="(question, qIndex) in questions" :key="question.q" v-show="questionsAwnsered === qIndex">
            <div class="question">{{ question.q }}</div>
            <div class="awnsers">
                <div class="awnser" v-for="awnser in question.awnsers" :key="awnser.text" @click.prevent="selectAwnser(awnser.isCorrect)">{{ awnser.text }}</div>
            </div>
        </div>
      </transition-group>
      
    </div>
</template>

<script>
export default {
    props: {
        questions: Array,
        questionsAwnsered: Number,
    },
    emits: ['questionAwnsered'],
    methods: {
        selectAwnser(isCorrect) {
            this.$emit('questionAwnsered', isCorrect);
        }
    }
}
</script>

