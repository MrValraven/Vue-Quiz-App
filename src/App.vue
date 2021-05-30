<template>
  <div class="ctr">
    <transition name="fade" mode="out-in">
      <Questions v-if="questionsAwnsered < questions.length" :questions="questions" :questionsAwnsered="questionsAwnsered" @questionAwnsered="questionAwnsered"/>
      <Result v-else :results="results" :totalCorrect="totalCorrect"/>
    </transition>
    
    <button type="button" class="reset-btn" @click.prevent="reset" v-if="questionsAwnsered === questions.length">Reset</button>

  </div>
</template>

<script>
import Questions from '@/components/Questions.vue';
import Result from '@/components/Result.vue';


export default {
  name: 'App',
  components: {
    Questions,
    Result,
  },
  data() {
    return {
      questionsAwnsered: 0,
      totalCorrect: 0,
      questions: [
        {
          q: "What is 2 + 2",
          awnsers: [
            {text: "4", isCorrect: true},
            {text: "3", isCorrect: false},
            {text: "Fish", isCorrect: false},
            {text: "5", isCorrect: false},
          ]
        },
        {
          q: "How many letters are in the word 'Banana'?",
          awnsers: [
            {text: "5", isCorrect: false},
            {text: "7", isCorrect: false},
            {text: "6", isCorrect: true},
            {text: "12", isCorrect: false},
          ]
        },
        {
          q: "Find the missing letter: C_ke",
          awnsers: [
            {text: "e", isCorrect: false},
            {text: "a", isCorrect: true},
            {text: "i", isCorrect: false},
          ]
        },
      ],
      
      results: [
        {min: 0, max: 2, title: "Try Again!", desc: "Do a little more studying and you may suceed!"},
        {min: 3, max: 3, title: "Wow, you're a genius!", desc: "Studying has definitely paid off for you!"},
      ]
    }
  },
  methods: {
    questionAwnsered(isCorrect) {

      if(isCorrect) {
        this.totalCorrect++;
      }

      this.questionsAwnsered++;
    },

    reset() {
      this.questionsAwnsered = 0;
      this.totalCorrect = 0;
    }
  }
}
</script>

<style lang="scss">

* {
  box-sizing: border-box;
}

body {
  font-size: 20px;
  font-family: sans-serif;
  padding-top: 20px;
  background: #e6ecf1;
}

.ctr {
  margin: 0 auto;
  max-width: 600px;
  width: 100%;
  box-sizing: border-box;
  position: relative;
}

.questions-ctr {
  position: relative;
  width: 100%;
}

.question {
  width: 100%;
  padding: 20px;
  font-size: 32px;
  font-weight: bold;
  text-align: center;
  background-color: #00ca8c;
  color: #fff;
  box-sizing: border-box;
}

.single-question {
  position: relative;
  width: 100%;
}

.awnser {
  border: 1px solid #8e959f;
  padding: 20px;
  font-size: 18px;
  width: 100%;
  background-color: #fff;
  transition: all 0.2s linear;
}

.awnser span {
  display: inline-block;
  margin-left: 5px;
  font-size: 0.75em;
  font-style: italic;
}

.progress {
  height: 50px;
  margin-top: 10px;
  background-color: #ddd;
  position: relative;
  }

.bar {
  height: 50px;
  background-color: #ff6372;
  transition: all 0.3s linear;
}

.status {
  position: absolute;
  top: 15px;
  left: 0px;
  text-align: center;
  color: #fff;
  width: 100%;
}

.awnser:not(.is-answered) {
  cursor: pointer;

  &:hover {
    background-color: #8ce200;
    border-color: #8ce200;
    color: #fff;
  }
}

.title {
  width: 100%;
  padding: 20px;
  font-size: 32px;
  font-weight: bold;
  text-align: center;
  background-color: #12cbc4;
  color: #fff;
  box-sizing: border-box;
}

.desc {
  border: 1px solid #8e959f;
  padding: 20px;
  text-align: center;
}

.fade-enter { 
  opacity: 0;
}

.fade-enter-active {
  transition: all 0.3s linear;
}

.fade-leave-active {
  transition: all 0.3s linear;
  opacity: 0;
  position: absolute;
}

.reset-btn {
  background-color: #ff6372;
  border: 0;
  font-size: 22px;
  color: #fff;
  padding: 10px 25px;
  margin: 10px auto;
  display: block;
}

.result {
  width: 100%;
}

.reset-btn:active, 
.reset-btn:focus,
.reset-btn:hover {
  border: 0;
  outline: 0;
}

</style>
