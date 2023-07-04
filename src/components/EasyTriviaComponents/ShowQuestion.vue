<template>
    <div v-if="type === 0" class="questionDesign">
        <div>{{shortQuestions[index].question}}</div>
        <div :class="['ans' , shortQuestions[index].ans1 === shortQuestions[index].correctAns ? 'right' : '' , shortQuestions[index].ans1 === shortQuestions[index].marked && shortQuestions[index].ans1 !== shortQuestions[index].correctAns ? 'wrong' : '']">1. {{shortQuestions[index].ans1}}</div>
        <div :class="['ans' , shortQuestions[index].ans2 === shortQuestions[index].correctAns ? 'right' : '' , shortQuestions[index].ans2 === shortQuestions[index].marked && shortQuestions[index].ans2 !== shortQuestions[index].correctAns ? 'wrong' : '']">2. {{shortQuestions[index].ans2}}</div>
        <div :class="['ans' , shortQuestions[index].ans3 === shortQuestions[index].correctAns ? 'right' : '' , shortQuestions[index].ans3 === shortQuestions[index].marked && shortQuestions[index].ans3 !== shortQuestions[index].correctAns ? 'wrong' : '']">3. {{shortQuestions[index].ans3}}</div>
        <div :class="['ans' , shortQuestions[index].ans4 === shortQuestions[index].correctAns ? 'right' : '' , shortQuestions[index].ans4 === shortQuestions[index].marked && shortQuestions[index].ans4 !== shortQuestions[index].correctAns ? 'wrong' : '']">4. {{shortQuestions[index].ans4}}</div>
    </div>

    <div v-if="type === 1" class="questionDesign">
        <div>{{longQuestions[index].question}}</div>
        <div :class="['ans' , longQuestions[index].ans1 === longQuestions[index].correctAns ? 'right' : '' , longQuestions[index].ans1 === longQuestions[index].marked && longQuestions[index].ans1 !== longQuestions[index].correctAns ? 'wrong' : '']">1. {{longQuestions[index].ans1}}</div>
        <div :class="['ans' , longQuestions[index].ans2 === longQuestions[index].correctAns ? 'right' : '' , longQuestions[index].ans2 === longQuestions[index].marked && longQuestions[index].ans2 !== longQuestions[index].correctAns ? 'wrong' : '']">2. {{longQuestions[index].ans2}}</div>
        <div :class="['ans' , longQuestions[index].ans3 === longQuestions[index].correctAns ? 'right' : '' , longQuestions[index].ans3 === longQuestions[index].marked && longQuestions[index].ans3 !== longQuestions[index].correctAns ? 'wrong' : '']">3. {{longQuestions[index].ans3}}</div>
        <div :class="['ans' , longQuestions[index].ans4 === longQuestions[index].correctAns ? 'right' : '' , longQuestions[index].ans4 === longQuestions[index].marked && longQuestions[index].ans4 !== longQuestions[index].correctAns ? 'wrong' : '']">4. {{longQuestions[index].ans4}}</div>
    </div>

    <div v-if="type === 2" class="questionDesign">
        <div>{{trueFalseQues[index].question}}</div>
        <div :class="['ans' , trueFalseQues[index].ans1 === trueFalseQues[index].correctAns ? 'right' : '' , trueFalseQues[index].ans1 === trueFalseQues[index].marked && trueFalseQues[index].ans1 !== trueFalseQues[index].correctAns ? 'wrong' : '']">1. {{trueFalseQues[index].ans1}}</div>
        <div :class="['ans' , trueFalseQues[index].ans2 === trueFalseQues[index].correctAns ? 'right' : '' , trueFalseQues[index].ans2 === trueFalseQues[index].marked && trueFalseQues[index].ans2 !== trueFalseQues[index].correctAns ? 'wrong' : '']">2. {{trueFalseQues[index].ans2}}</div>
    </div>

    <div v-if="type === 3" class="questionDesign">
        <form>
            <div>{{numberQues[0].question}}</div>
            <br>
            <label>א. {{numberQues[0].ans1}} {{space}}</label>
            <select :class="[numberQues[0].correctAns[0]===numberQues[0].marked[0] ? 'rightOp' : 'wrongOp']" disabled>
                <option>{{numberQues[0].marked[0] }}</option>
            </select>
            <br>
            <label>ב. {{numberQues[0].ans2}} {{space}}</label>
            <select :class="[numberQues[0].correctAns[1]===numberQues[0].marked[1] ? 'rightOp' : 'wrongOp']" disabled>
                <option>{{numberQues[0].marked[1] }}</option>
            </select>
            <br>
            <label>ג. {{numberQues[0].ans3}} {{space}}</label>
            <select :class="[numberQues[0].correctAns[2]===numberQues[0].marked[2] ? 'rightOp' : 'wrongOp']" disabled>
                <option>{{numberQues[0].marked[2]}}</option>
            </select>
            <br>
            <label>ד. {{numberQues[0].ans4}} {{space}}</label>
            <select :class="[numberQues[0].correctAns[3]===numberQues[0].marked[3] ? 'rightOp' : 'wrongOp']" disabled>
                <option>{{numberQues[0].marked[3]}}</option>
            </select>
        </form>  
    </div>

    <button @click="back">חזור</button>
</template>

<script>
export default {
    props : ["number" ,"lengthArray", "shortQuestions", "longQuestions", "trueFalseQues", "numberQues", "order"],
    data () {
        return {
            index : '',
            type: '',
            space: "           ",
        };
    },
    methods : {
        back () {
            this.$emit('back');
        }
    },
    mounted () {
        console.log(this.lengthArray);
        console.log(this.number);
        if (this.number <= this.lengthArray[0] ) { // short questions
            this.index = this.number;
            this.type = 0;
        } else if (this.number <= (this.lengthArray[1]+this.lengthArray[0])) { // long questions
            this.index = this.number - this.lengthArray[0];
            this.type = 1;
        } else if (this.number <= (this.lengthArray[2]+this.lengthArray[1]+this.lengthArray[0]-1)) { // true/false questions
            this.index = this.number - this.lengthArray[1]- this.lengthArray[0];
            this.type = 2;

        } else { // number question
            this.index = 51;
            this.type = 3;
        }
        console.log(this.type);
    }

};
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

.right {
    background-color: green;
}

.wrong {
    background-color: red;
}

.rightOp{
    color: black;
   background: green;
}

.wrongOp {
    color: black;
    background: red;
}
</style>