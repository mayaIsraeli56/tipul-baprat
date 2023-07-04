<template>
  <!-- <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/>
  </div> -->
  <!-- <ol dir="rtl">
    <li class="try111" v-for="ques in shortQues" :key="ques.question">{{ques.question}}
      <div>א. {{ques.ans1}}</div>
      <div>ב. {{ques.ans2}}</div>
      <div>ג. {{ques.ans3}}</div>
      <div>ד. {{ques.ans4}}</div>
      <div> תשובה נכונה : {{ques.correctAns}}</div>
      <br>
    </li>
  </ol> -->
<EasyTrivia></EasyTrivia>
  <div >
  </div>
</template>

<script>
import easyQuestion from '@/data/easyQuestion.json'
import EasyTrivia from '@/components/EasyTriviaComponents/EasyTrivia.vue'

export default ({
  data() {
   return {
    shortQues : easyQuestion.shortQues,
    longQues : easyQuestion.longQues,
    trueFalseQues : easyQuestion.trueFalseQues,
    dragQues : easyQuestion.dragQues,
   };
  },
  components : {
    EasyTrivia,
  }
})

// @ is an alias to /src
// import HelloWorld from '@/components/HelloWorld.vue'

// export default {
//   name: 'HomeView',
//   components: {
//     HelloWorld
//   }
// }
</script>
<style scoped>
.try111 {
  text-align: right ;
}
</style>
