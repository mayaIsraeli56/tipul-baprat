<template>
    <div v-if="stage === 0" class="questionDesign">
        <div>sumCorrectAns: {{sumCorrectAns}}</div>
        <div>sumQues: {{sumQues}}</div>
        <button id="back" class="btn" @click="tryAgain">אני רוצה לנסות שוב</button>
        <button id="next" class="btn" @click="learn">בא ל ללמוד מהטעויות שלי!</button>
    </div>
    <pickQuestion v-if="stage === 1" :sumQues="sumQues" :lengthArray="lengthArray" :shortQuestions="shortQuestions" :longQuestions="longQuestions" :trueFalseQues="trueFalseQues" :numberQues="numberQues"></pickQuestion>

</template>

<script>
import PickQuestion from '@/components/EasyTriviaComponents/PickQuestion.vue'

export default {
    props : ["sumTrueAns","lengthArray", "shortQuestions", "longQuestions", "trueFalseQues", "numberQues"],
    components: {
        PickQuestion,
    },
    data() {
        return {
            sumCorrectAns : 0,
            sumQues: 0,
            stage : 0,
        };
    }, 
    methods : {
        sumArray (arr) {
            let sum = 0;
            for(let i = 0; i<arr.length; i++) {
                sum+=arr[i];
            }
            return sum;
        },
        tryAgain () {
            this.$emit('try-again');
        },
        learn () {
            this.stage++;
        }

    },
    mounted() {
        this.sumCorrectAns = this.sumArray(this.sumTrueAns);
        this.sumQues = this.sumArray(this.lengthArray)+4;
    }
}
</script>

<style scoped>

.questionDesign {
    text-align: right;
    background-color: pink ;
    border-radius: 0.2vw;
    margin: 0.5vh;
    padding: 2vw;
    display: inline-block;
    direction: rtl;
}

.btn {
    background-color: pink ;
    width: fit-content;
    direction: rtl;
    padding: 1vh;
    position: absolute;
    left: 46.5vw;
    margin-top: 2vh;
    cursor: pointer;
    border-radius: 0.4vw ;
}

.btn:hover {
    background-color: rgb(253, 215, 221) ;
}

#next {
    top: 18vh;
    left: 40.8vw;
}

#back {
    top: 18vh;
    left: 50.6vw;
}
</style>