<template>
    <div class="previewContainer" >
        <div style="position:relative;">
            <img width="380" height="380" src="../assets/front.png" alt="">
            <img v-show="location.includes(0)"
                 style="position: absolute; margin: auto;top: 0;left: 0;right: 0;bottom: 0;"
                 :src="imgUrl.url" alt=""></div>
        <div style="position:relative;">
            <img width="380" height="380" src="../assets/back.png" alt="">
            <img v-show="location.includes(1)"
                 style="position: absolute; margin: auto;top: 0;left: 0;right: 0;bottom: 0;"
                 :src="imgUrl.url" alt=""></div>
    </div>

</template>
<script>
    export default {
        name: 'Preview',
        props: {
            imgUrl: Object,
            location: Array
        },
        data() {
            return {}
        }
    }
</script>
<style scoped>

    .previewContainer {
        /*width: 100%;*/
        /*height: calc(100% - 290px);*/
        background: greenyellow;
        display: flex;
        justify-content: center;
    }
.previewContainer div{
    margin: 5px;
}
</style>
