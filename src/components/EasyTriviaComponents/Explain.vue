<template>
    <div class="text">
        <div class="headline">צוער/ת יקר/ה,</div>
        <div class="center">לפניך מבחן בנושא טיפול בפרט.</div>
        <div class="center">במבחן יש 52 שאלות, מתוכן:  </div>
        <ul class="list">
            <li>שאלות אמריקאיות</li>
            <li>שאלות נכון/ לא נכון</li>
            <li>שאלת מספור פעולות</li>
        </ul>
        <div class="center"> ניתן לעבור לשאלה הבאה רק לאחר שענית על השאלה הנוכחית. ישנה אופציה לחזור אחורה לשאלות שכבר עשית.</div>
        <div class="center">בסוף המבחן אפשר ללמוד מהטעויות. </div>
         <div> ניתן להיבחן יותר פעם אחת.</div>
    </div>
    <div class="goodluck">בהצלחה!</div>
    <div @click="startTest" class="startBtn">שנתחיל?</div>
</template>

<script>
export default ({
    data() {
     return {

     };
    },
    methods: {
        startTest () {
            this.$emit('start-test');
        }
    }
  })
</script>

<style scoped>
.startBtn{
    background-image: url("@/assets/shortQuesIcons/shortBubbleIcon.png");
    background-repeat: no-repeat;
    background-size: contain;
    background-position-x: center;
    background-position-y: center;
    font-size: 170%;
    padding: 15%;
    height: fit-content;
    position: relative;
    top: 1%;
    left: 50%;
    transform: translateX(-50%);
}


.text{
    margin-top: 15%;
    font-size: 2rem;
    padding: 2.5rem;
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
}

.goodluck{
    margin-bottom: 2%;
    font-size: 2.3rem;
}

.headline{
    margin-top: -15%;
    font-size: 3rem ;
    line-height: 140%;
}

.list{
    margin-top: 4%;
    margin-bottom: 4%;
    font-size: 1.7rem;
}
</style>