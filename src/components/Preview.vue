<template>
    <div><img src="imgUrl" alt=""></div>
</template>
<script>
    export default {
        name: 'Preview',
        props: {url: String},
        data(){
            return{
                imgUrl:this.url
            }
        }
    }
</script>
<style scoped>

    .container header {
        font-size: 20px;
        font-weight: 600;
        margin: 0 0 -25px 0;
    }

    .form-outer form {
        display: flex;
        width: 500%;
    }

    .form-outer form .page .field input {
        height: 100%;
        width: 100%;
        border: 1px solid lightgrey;
        border-radius: 5px;
        font-size: 10px;
        padding-left: 15px;
    }

    .form-outer form .page .field button {
        width: 100%;
        height: calc(100% + 5px);
        margin-top: -20px;
        border: none;
        border-radius: 5px;
        background: #403D75;
        color: #fff;
        font-size: 18px;
        font-weight: 600;
        letter-spacing: 1px;
        text-transform: uppercase;
        cursor: pointer;
    }

    .form-outer form .page .field button:hover {
        background: #262447;
    }

    .form-outer form .page .btns button {
        margin-top: -20px !important;
    }

    form .page .btns button {
        margin-right: 3px;
        font-size: 17px;
    }


    .progress-bar .step p {
        font-size: 12px;
        font-weight: 500;
        color: #262445;
        margin-bottom: 8px;
        transition: 0.2s;
    }


    .progress-bar .step.bullet span {
        font-weight: 300;
        font-size: 14px;
        line-height: 20px;
        position: absolute;
        left: 50%;
        transform: translateX(-50%);
    }

    .progress-bar .step .bullet.active span {
        display: none;
    }

    @keyframes animate {
        100% {
            transform: scaleX(1)
        }
    }


    .inline-labels div {
        display: flex;
        padding: 2px;
    }

    .printPosition i {
        color: #ccc;
    }

    .printPosition span {
        color: #ccc;
        font-size: 14px;
        font-weight: 600;
    }

    .printPosition.active i {
        color: darkgreen;
    }

    .printPosition.active span {
        color: darkgreen;
        font-size: 14px;
        font-weight: 600;
    }
</style>
