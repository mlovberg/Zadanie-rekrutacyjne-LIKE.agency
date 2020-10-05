<template>
    <div class="previewContainer">
        <div style="position:relative;">
            <img width="380" height="380" src="../assets/front.png" alt="">
            <img class="print" v-show="printSide.includes(0)"
                 :src="imgUrl" alt="">
        </div>
        <div style="position:relative;">
            <img width="380" height="380" src="../assets/back.png" alt="">
            <img class="print" v-show="printSide.includes(1)"
                 :src="imgUrl" alt="">
        </div>
        <div v-if="price&&price>0" class="price"><div>{{price}}</div></div>
    </div>

</template>i
<script>
    export default {
        name: 'Preview',
        props: {
            imgUrl: String,
            printSide: Array,
            price:Number
        }
    }
</script>
<style scoped>

    .previewContainer {
        display: flex;
        justify-content: center;
    }

    .previewContainer div {
        margin: 5px;
    }

     .print {
        position: absolute;
        margin: auto;
        top: 0;
        left: 0;
        right: 0;
        bottom: 0;
    }

    .price{
        width:100px;
        height:100px;
        border-radius: 50px;
        background: limegreen;
        border-color: green;
        font-size: 40px;
        font-weight: bold;
    }

    .price div{
        margin-top:30px;
        color:#262447;
    }
</style>
