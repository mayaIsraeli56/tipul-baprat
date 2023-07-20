<template>
  <EasyTrivia></EasyTrivia>
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
</style>
