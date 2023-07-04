<template>
    <div v-if="!showQues" class="questionDesign">
        <button v-for="btn in sumQues" :key="btn" :class="['btn', checkAns[btn] ? 'right' : 'wrong']" @click="picked(btn)">{{btn}}</button>
    </div>
    <ShowQuestion v-else :number="number" :lengthArray="lengthArray" :shortQuestions="shortQuestions" :longQuestions="longQuestions" :trueFalseQues="trueFalseQues" :numberQues="numberQues" @back="back"></ShowQuestion>
</template>

<script>
import ShowQuestion from '@/components/EasyTriviaComponents/ShowQuestion.vue'

export default {
    props : ["sumQues","lengthArray", "shortQuestions", "longQuestions", "trueFalseQues", "numberQues"],
    components : {
        ShowQuestion,
    },
    data() {
        return {
            checkAns : [true],
            showQues: false,
            number : '',
        };
    }, 
    methods : {
        picked(ansNum) {
            this.number = (ansNum-1);
            console.log(this.number)
            this.showQues = true;
        },
        back () {
            this.showQues = false;
        }
    },
    mounted () {
        this.lengthArray[0]++;
        this.lengthArray[1]++;
        this.lengthArray[2]++;
        for (let i = 0; i< this.lengthArray[0]; i++) { // check the short questions
                if(this.shortQuestions[i].marked === this.shortQuestions[i].correctAns) {
                    this.checkAns.push(true);
                } else {
                    this.checkAns.push(false);
                }
        }
        for (let i = 0; i< this.lengthArray[1]; i++) { // check the long questions
                if(this.longQuestions[i].marked === this.longQuestions[i].correctAns) {
                    this.checkAns.push(true);
                } else {
                    this.checkAns.push(false);
                }
        }
        for (let i = 0; i< this.lengthArray[2]; i++) { // check the true/false questions
                if(this.trueFalseQues[i].marked === this.trueFalseQues[i].correctAns) {
                    this.checkAns.push(true);
                } else {
                    this.checkAns.push(false);
                }
        }
        this.checkAns.push(true); // check the number question
        for(let i=0; i<4; i++) {
                    if(this.numberQues[0].marked[i] !== this.numberQues[0].correctAns[i]) {
                        this.checkAns[52] = false;
                    }
        }
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
    display: flex;
    width: 30vw;
    flex-flow: row;
    flex-wrap: wrap;
    direction: rtl;
    position: absolute;
    left: 35vw;
}

.btn {
    text-align: center;
    position: relative;
    margin: 1vw;
    width: 5vw;
    height: 5vh;
    cursor: pointer;
}

.wrong{
    background-color: red;
}

.right{
    background-color: green;
}

</style>