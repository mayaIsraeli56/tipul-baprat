<template>
    <div dir="rtl" class="questionDesign">
        <div>{{count+1}}) {{shortQuestions[count].question}}</div>
        <div @click="clickAns(shortQuestions[count].ans1)" :class="['ans', shortQuestions[count].ans1 === shortQuestions[this.count].marked ? 'marked' : '' ]">1. {{shortQuestions[count].ans1}}</div>
        <div @click="clickAns(shortQuestions[count].ans2)" :class="['ans', shortQuestions[count].ans2 === shortQuestions[this.count].marked ? 'marked' : '' ]">2. {{shortQuestions[count].ans2}}</div>
        <div @click="clickAns(shortQuestions[count].ans3)" :class="['ans', shortQuestions[count].ans3 === shortQuestions[this.count].marked ? 'marked' : '' ]">3. {{shortQuestions[count].ans3}}</div>
        <div @click="clickAns(shortQuestions[count].ans4)" :class="['ans', shortQuestions[count].ans4 === shortQuestions[this.count].marked ? 'marked' : '' ]">4. {{shortQuestions[count].ans4}}</div>
    </div>
    <button id="next" class="btn" v-if="shortQuestions[this.count].marked !== '' " @click="nextQues">שאלה הבאה</button>
    <button id="back" class="btn" v-if="count>0" @click="count--" >שאלה אחורה</button>
    <div>תשובות נכונות : {{countT}}</div>
    <div>תשובות לא נכונות : {{countF}}</div>

</template>

<script>

export default {
    props : ["count1","shortQuestions"],
    data() {
        return {
           count: 0,
           maxCount: this.shortQuestions.length-1,
           countT: 0,
           countF: 0,
        };
    }, 
    methods : {
        clickAns (ans) {
            this.shortQuestions[this.count].marked = ans;
            this.check();
        },
        check () {
            this.countT = 0;
            for ( let i = 0; i < this.shortQuestions.length; i++) {
                if(this.shortQuestions[i].marked === this.shortQuestions[i].correctAns) {
                    this.countT++;
                }
            }
            this.countF = this.shortQuestions.length - this.countT;
        },
        nextQues () {
            if (this.count < this.maxCount) {
                this.count++;
            } else {
                this.$emit('finish', this.countT);
            }
        }
    } ,
    mounted () {
        this.count = this.count1;
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

.ans {
    margin-top: 1vh;
    cursor: pointer;
    padding: 0.5vh;
    border-radius: 0.2vh;
}

.ans:hover {
    background-color: rgb(253, 215, 221) ;
}

.marked {
    background-color: rgb(247, 128, 146) ;
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
    top: 32vh;
    left: 39.8vw;
}

#back {
    top: 32vh;
    left: 55.6vw;
}
</style>