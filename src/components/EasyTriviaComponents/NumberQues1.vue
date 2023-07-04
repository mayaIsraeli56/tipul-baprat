<template>
    <div dir="rtl" class="questionDesign">
        <form>
            <div>{{startPoint+1}}) {{numberQues[0].question}}</div>
            <br>
            <label>א. {{numberQues[0].ans1}} {{space}}</label>
            <select v-model="order[0]"  @click="check">
                <option value="1">1</option>
                <option value="2">2</option>
                <option value="3">3</option>
                <option value="4">4</option>
            </select>
            <br>
            <label>ב. {{numberQues[0].ans2}} {{space}}</label>
            <select v-model="order[1]"  @click="check">
                <option value="1">1</option>
                <option value="2">2</option>
                <option value="3">3</option>
                <option value="4">4</option>
            </select>
            <br>
            <label>ג. {{numberQues[0].ans3}} {{space}}</label>
            <select v-model="order[2]"  @click="check">
                <option value="1">1</option>
                <option value="2">2</option>
                <option value="3">3</option>
                <option value="4">4</option>
            </select>
            <br>
            <label>ד. {{numberQues[0].ans4}} {{space}}</label>
            <select v-model="order[3]" @click="check">
                <option value="1">1</option>
                <option value="2">2</option>
                <option value="3">3</option>
                <option value="4">4</option>
            </select>
        </form>
        <div>{{countT}}</div>
    </div>
    <button id="next" class="btn" v-if="checkMarkAll" @click="finished">סיימתי</button>
    <button id="back" class="btn" @click="previousQues" >שאלה אחורה</button>
    <div>תשובות נכונות : {{countT}}</div>
    <div>תשובות לא נכונות : {{countF}}</div>

</template>

<script>


export default {
    props : ["numberQues","startPoint"],
    data() {
        return {
           countT: 1,
           order: ["","","",""],
           space: "           ",
        };
    }, 
    methods : {
        previousQues () {
            this.$emit('go-back');
        },
        check(){
            this.countT = 1;
            if(this.checkMarkAll) {
                for(let i=0; i<4; i++) {
                    if(this.order[i] !== this.numberQues[0].correctAns[i]) {
                        this.countT = 0;
                    }
                }
            }
        }, 
        finished () {
            this.$emit('submitTrivia', this.countT);
        }
    }, 
    computed: {
        checkMarkAll() {
            if (this.order[0] !== "" && this.order[1] !== "" && this.order[2] !== "" && this.order[3] !== "") {
                return true ;
            }
            return false;
        }
    },
    mounted () {
        this.order = this.numberQues[0].marked;
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