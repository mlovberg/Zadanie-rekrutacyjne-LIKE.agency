<template>
    <div id="orderForm">
        <link rel="stylesheet"
              href="https://use.fontawesome.com/releases/v5.2.0/css/all.css"
              integrity="sha384-hWVjflwFxL6sNzntih27bfxkr27PmbbK/iSvJ+a4+0owXq79v+lsFkW54bOGbiDQ"
              crossorigin="anonymous">

        <div class="container">
            <!--            <header>Login form</header>-->
            <div class="progress-bar">
                <div class="step">
                    <p :class="page>0? 'active' : ''">Miejsce</p>
                    <div :class="[ page > 0 ? 'bullet active' : 'bullet' ]">
                        <span>1</span>
                    </div>
                    <div :class="['check fas fa-check', page>0? ' active' : '']"></div>
                </div>
                <div class="step">
                    <p :class="page>1? 'active' : ''">Nadruk</p>
                    <div :class="[ page > 1 ? 'bullet active' : 'bullet' ]">
                        <span>2</span>
                    </div>
                    <div :class="['check fas fa-check', page>1? ' active' : '']"></div>
                </div>
                <div class="step">
                    <p :class="page>2? 'active' : ''">Dostawa</p>
                    <div :class="[ page > 2 ? 'bullet active' : 'bullet' ]">
                        <span>3</span>
                    </div>
                    <div :class="['check fas fa-check', page>2? ' active' : '']"></div>
                </div>
                <div class="step">
                    <p :class="page>3? 'active' : ''">Podsumowanie</p>
                    <div :class="[ page > 3 ? 'bullet active' : 'bullet' ]">
                        <span>4</span>
                    </div>
                    <div :class="['check fas fa-check', page>3? ' active' : '']"></div>
                </div>
                <div class="step">
                    <p :class="page>4? 'active' : ''">Koniec</p>
                    <div :class="[ page > 4 ? 'bullet active' : 'bullet' ]">
                        <span>5</span>
                    </div>
                    <div :class="['check fas fa-check', page>4? ' active' : '']"></div>
                </div>
            </div>
            <div class="form-outer">
                <form action="#">
                    <div class="page" :style="pageMarginStyle">
                        <p style="margin-top: 20px;">Wybierz miejsce nadruku</p>
                        <div style="display: flex;justify-content: space-around; height: 70px; width: 85%; margin-top: 30px">

                            <div v-for="pos in positions" :key="pos.id"
                                 :class="['printPosition', selectedPositions.includes(pos.id) ? 'active':'']"
                                 style="display: grid">
                                <i class="fas fa-check-circle fa-3x " @click="selectPosition(pos.id)"></i>
                                <span>{{pos.name}}</span>
                            </div>

                        </div>
                        <div class="field btns">
                            <button :disabled="!selectedPositions.length" @click="slide(1)">Dalej</button>
                        </div>
                    </div>
                    <div class="page">
                        <div style="height: 140px; width: 85%;">
                            <div>
                                <div style="position:relative;">
                                    <i style="position:absolute; left:85px;top:30px;"
                                       :class="['fas fa-caret-left fa-3x', previousImageAvailable()  ? '' : 'gray' ]"
                                       @click="setPreviousImage">
                                    </i>

                                    <img width="100px" height="100px" :src="imgUrl.url" alt="">
                                    <i style="position:absolute; right:85px;top:30px;"
                                       :class="['fas fa-caret-right fa-3x', nextImageAvailable()  ? '' : 'gray' ]"
                                       @click="setNextImage">
                                    </i>
                                </div>
                            </div>
                            <i class="fas fa-sync-alt fa-2x" @click="reloadImage"></i>
                        </div>
                        <div class="field btns">
                            <button @click="slide(0)">Cofnij</button>
                            <button @click="slide(2)">Dalej</button>
                        </div>
                    </div>
                    <div class="page">
                        <div class="field inline-labels">

                            <div style="width:50%">
                                <!--                            <div class="label">Imię</div>-->
                                <input v-model:="user.name" type="text" class="text" placeholder="Imię"></div>
                            <div style="width:50%">
                                <!--                            <div class="label">Nazwisko</div>-->
                                <input v-model:="user.surname" type="text" class="text" placeholder="Nazwisko"></div>
                        </div>
                        <div class="field inline-labels">
                            <div style="width:60%">
                                <!--                                <div class="label ">Ulica</div>-->
                                <input v-model:="user.street" type="text" class="text" placeholder="Ulica">
                            </div>
                            <div style="width:20%">
                                <!--                                <div class="label ">bud</div>-->
                                <input v-model:="user.house" type="number" class="text" placeholder="budynek">
                            </div>
                            <div style="width:20%">
                                <!--                                <div class="label">m</div>-->
                                <input v-model:="user.flat" type="number" class="text" placeholder="mieszkanie">
                            </div>
                        </div>

                        <div class="field">
                            <!--                            <div class="label">Telefon</div>-->
                            <input v-model:="user.phone" type="text" class="text" placeholder="telefon">
                        </div>
                        <div class="field">
                            <!--                            <div class="label">e-mail</div>-->
                            <input v-model:="user.email" type="text" class="text" placeholder="email">
                        </div>
                        <div class="field btns">
                            <button @click="slide(1)">Cofnij</button>
                            <button @click="slide(3)">Dalej</button>
                        </div>
                    </div>
                    <div class="page">
                        <div style="height: 140px;"></div>
                        <div class="field btns">
                            <button @click="slide(2)">Cofnij</button>
                            <button @click="slide(4)">Dalej</button>
                        </div>
                    </div>
                    <div class="page">
                        <div style="height: 140px;"></div>

                        <div class="field btns">
                            <button @click="slide(3)">Cofnij</button>
                            <button class="submit" @click="page=5">Submit</button>
                        </div>
                    </div>

                </form>
            </div>
        </div>
        <Preview :imgUrl="imgUrl" :location="selectedPositions"/>
    </div>
</template>

<script>
    import Preview from "@/components/Preview";
    import * as _ from "underscore";

    export default {
        name: "OrderForm",
        components: {Preview},
        data() {
            return {
                pageMarginStyle: "margin-left: 0px;",
                page: 0,
                user: {
                    name: "",
                    surname: "",
                    street: "",
                    house: -1,
                    flat: -1,
                    phone: -1,
                    email: ""
                },
                positions: [
                    {id: 0, name: 'Przód'},
                    {id: 1, name: 'Tył'}
                ],
                selectedPositions: [],
                imgUrl: null,
                previousImg: "",
                selectedImages: []
            }
        },
        mounted() {
            this.reloadImage()
        },
        // watch: {
        //     imgUrl: function (newVal, oldVal) {
        //         if (newVal !== oldVal) {
        //             this.previousImg = oldVal;
        //         }
        //     }
        // },
        methods: {
            slide: function (page) {
                let margin = -400 * page;
                this.pageMarginStyle = `margin-left: ${margin}px;`;
                this.page = page;
            }
            ,
            selectPosition: function (positionId) {
                if (this.selectedPositions.includes(positionId)) {
                    this.selectedPositions.splice(this.selectedPositions.indexOf(positionId))
                } else {
                    this.selectedPositions.push(positionId);
                }
            },
            reloadImage: function () {
                fetch("https://picsum.photos/150", {method: 'GET'})
                    .then((response) => {
                        this.imgUrl = {id: _.uniqueId() * 1, url: response.url};
                        this.selectedImages.push(this.imgUrl);
                    });
            },
            setPreviousImage: function () {
                this.imgUrl = _.findWhere(this.selectedImages, {id: this.imgUrl.id - 1});
            }, setNextImage: function () {
                this.imgUrl = _.findWhere(this.selectedImages, {id: this.imgUrl.id + 1});
            },
            previousImageAvailable: function () {
                return _.any(this.selectedImages, (img) => {
                    return img.id < this.imgUrl.id;
                })
            },
            nextImageAvailable: function () {
                return _.any(this.selectedImages, (img) => {
                    return img.id > this.imgUrl.id;
                })
            }
        }
    }
</script>

<style scoped>
    #orderForm {
        justify-content: center;
        background: -webkit-linear-gradient(bottom, aliceblue, #9B96F2);
    }

    .container {
        display: inline-block;
        width: 400px;
        height: 200px;
        background: #fff;
        border-radius: 5px;
        text-align: center;
        padding: 20px 0px 45px 70px;
        overflow: hidden;
    }

    /*.container header {*/
    /*    font-size: 20px;*/
    /*    font-weight: 600;*/
    /*    margin: 0 0 -25px 0;*/
    /*}*/

    .container .form-outer {
        width: 100%;
        overflow: hidden;
    }

    .form-outer form {
        display: flex;
        width: 500%;
    }

    .form-outer form .page {
        width: 20%;
        transition: margin-left 0.3s ease-in-out;
        position: relative;
    }

    .form-outer form .page .title {
        text-align: left;
        font-weight: 500;
        font-size: 25px;
    }

    .form-outer form .page .field {
        height: 25px;
        width: 330px;
        margin: 10px 0;
        display: flex;
        position: relative;
    }

    /*.form-outer form .page .field .label {*/
    /*    position: absolute;*/
    /*    top: -18px;*/
    /*    font-weight: 500;*/
    /*}*/

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

    .form-outer form .page .field button:disabled:hover {
        background: #ccc;
    }

    form .page .btns {
        position: absolute;
        bottom: 0px;
    }

    form .page .btns button {
        margin-right: 3px;
        font-size: 17px;
    }

    form .page .btns button:disabled {
        margin-right: 3px;
        font-size: 17px;
        background: #ccc;
    }


    .container .progress-bar {
        display: flex;
    }

    .container .progress-bar .step {
        text-align: center;
        width: 17%;
        position: relative;
        margin-bottom: 5px;
    }

    .progress-bar .step p {
        font-size: 12px;
        font-weight: 500;
        color: #262445;
        margin-bottom: 8px;
        transition: 0.2s;
    }

    .progress-bar .step p.active {
        color: #9B96F2;
    }


    .progress-bar .step .bullet {
        position: relative;
        height: 35%;
        width: 35%;
        border: 3px solid #AEAEBD;
        display: inline-block;
        border-radius: 50%;
        transition: 0.2s;
    }

    .progress-bar .step .bullet.active {
        border-color: #9B96F2;
        background: #9B96F2;
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

    .progress-bar .step .check.active {
        display: block;
        color: #fff;
    }

    .progress-bar .step:last-child .bullet:before,
    .progress-bar .step:last-child .bullet:after {
        display: none;

    }

    .progress-bar .step .bullet:before,
    .progress-bar .step .bullet:after {
        position: absolute;
        content: '';
        bottom: 8px;
        right: -44px;
        height: 3px;
        width: 40px;
        background: #AEAEBD;
    }

    .progress-bar .step .bullet.active:after {
        background: #9B96F2;
        transform: scaleX(0);
        animation: animate 0.3s linear forwards;
        transform-origin: left;
    }

    @keyframes animate {
        100% {
            transform: scaleX(1)
        }
    }


    .progress-bar .step .check {
        position: absolute;
        left: 50%;
        top: 85%;
        font-size: 15px;
        transform: translate(-50%, -50%);
        display: none;
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

    .gray {
        color: #ccc;
    }
</style>
