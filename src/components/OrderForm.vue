<template>
    <div id="orderForm">
        <link rel="stylesheet"
              href="https://use.fontawesome.com/releases/v5.2.0/css/all.css"
              integrity="sha384-hWVjflwFxL6sNzntih27bfxkr27PmbbK/iSvJ+a4+0owXq79v+lsFkW54bOGbiDQ"
              crossorigin="anonymous">
        <div class="center">
            <div class="ellipse">
                <div class="container">
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
                            <p :class="page>2? 'active' : ''">Podsumowanie</p>
                            <div :class="[ page > 2 ? 'bullet active' : 'bullet' ]">
                                <span>4</span>
                            </div>
                            <div :class="['check fas fa-check', page>2? ' active' : '']"></div>
                        </div>
                        <div class="step">
                            <p :class="page>3? 'active' : ''">Koniec</p>
                            <div :class="[ page > 3 ? 'bullet active' : 'bullet' ]">
                                <span>5</span>
                            </div>
                            <div :class="['check fas fa-check', page>3? ' active' : '']"></div>
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
                                <div class="field inline-labels ">

                                    <div style="width:50%" class="form-group"
                                         :class="{'form-group--error': $v.user.name.$error }">
                                        <input v-model.trim="$v.user.name.$model" type="text" class="text form__input"
                                               placeholder="imię">
                                    </div>
                                    <div style="width:50%" class="form-group"
                                         :class="{'form-group--error': $v.user.surname.$error }">
                                        <input v-model.trim="$v.user.surname.$model" type="text" class="text"
                                               placeholder="nazwisko"></div>
                                </div>
                                <div class="field inline-labels">
                                    <div style="width:60%" class="form-group"
                                         :class="{'form-group--error': $v.user.street.$error }">
                                        <input v-model.trim="$v.user.street.$model" type="text" class="text"
                                               placeholder="ulica">
                                    </div>
                                    <div style="width:20%" class="form-group"
                                         :class="{'form-group--error': $v.user.house.$error }">
                                        <input v-model="$v.user.house.$model" type="text" class="text"
                                               placeholder="budynek">
                                    </div>
                                    <div style="width:20%" class="form-group"
                                         :class="{'form-group--error': $v.user.flat.$error }">
                                        <input v-model="$v.user.flat.$model" type="text" class="text"
                                               placeholder="mieszkanie">
                                    </div>
                                </div>
                                <div class="field form-group"
                                     :class="{'form-group--error': $v.user.phone.$error }">
                                    <input v-model.trim="$v.user.phone.$model" type="text" class="text"
                                           placeholder="telefon">
                                </div>
                                <div class="field form-group"
                                     :class="{'form-group--error': $v.user.email.$error }">
                                    <input v-model.trim="$v.user.email.$model" type="text" class="text"
                                           placeholder="email">
                                </div>
                                <div class="field btns">
                                    <button @click="slide(1)">Cofnij</button>
                                    <button :disabled="$v.user.$invalid" @click="slide(3)">Dalej</button>
                                </div>
                            </div>
                            <div class="page">
                                <div class="confirmation">
                                    <div class="confirmationSection ">
                                        <div><b>Podsumowanie zamówienia:</b></div>
                                        <div class="leftFloat"><span>T-shirt biały , nadruk: {{posNames}}</span></div>
                                        <div class="rightFloat"><span> {{price}} jedn.</span></div>
                                    </div>
                                    <div class="confirmationSection">
                                        <div><b>Dostawa</b></div>
                                        <div class="leftFloat">Zamawiający:</div>
                                        <div class="rightFloat"> {{user.name}} {{user.surname}}</div>
                                        <div class="leftFloat">Adres:</div>
                                        <div class="rightFloat"> {{user.street}} {{user.house}}, m. {{user.flat}}</div>
                                        <div class="leftFloat">Telefon:</div>
                                        <div class="rightFloat">{{user.phone}}</div>
                                        <div class="leftFloat">Email:</div>
                                        <div class="rightFloat lowercase"> {{user.email}}</div>
                                    </div>

                                </div>
                                <div class="field btns">
                                    <button @click="slide(2)">Cofnij</button>
                                    <button class="makeOrderButton" @click="order">Złóż zamówienie</button>
                                </div>
                            </div>
                            <div class="page">
                                <div style="height: 140px; width:85%; ">
                                    <p>Dziękujemy! Twoje zamówienie zostało złożone.</p>
                                    <p><b>Informacje na temat zamówienia:</b></p>

                                    <table class="orderConfirmation">
                                        <tr>
                                            <th>Zamawiający</th>
                                            <td>{{user.name}} {{user.surname}}</td>
                                        </tr>
                                        <tr>
                                            <th>Dostawa</th>
                                            <td>{{user.street}} {{user.house}}, m. {{user.flat}}</td>
                                        </tr>
                                        <tr>
                                            <th></th>
                                            <td>{{user.phone}}</td>
                                        </tr>
                                        <tr>
                                            <th></th>
                                            <td>{{user.email}}</td>
                                        </tr>
                                    </table>
                                </div>

                            </div>

                        </form>
                    </div>
                </div>
            </div>
        </div>
        <Preview :imgUrl="imgUrl.url" :printSide="selectedPositions" :price="price"></Preview>
    </div>
</template>

<script>
    import * as _ from "underscore";
    import {required, minLength} from 'vuelidate/lib/validators'
    import Vue from 'vue';
    import {Vuelidate} from "vuelidate";
    import email from "vuelidate/lib/validators/email";
    import alpha from "vuelidate/lib/validators/alpha";
    import numeric from "vuelidate/lib/validators/numeric";
    import Preview from "@/components/Preview";

    Vue.use(Vuelidate);

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
                    house: "",
                    flat: "",
                    phone: "",
                    email: ""
                },
                positions: [
                    {id: 0, name: 'Przód'},
                    {id: 1, name: 'Tył'}
                ],
                selectedPositions: [],
                imgUrl: {id: Number, url: ''},
                previousImg: "",
                selectedImages: []
            }
        },
        computed: {
            posNames: function () {
                return _.pluck(this.selectedPositions, 'name').join(' i ').toLowerCase()
            },
            price: function () {
                return this.selectedPositions.length * 10;
            }
        },
        validations() {
            return {
                user: {
                    name: {
                        required,
                        alpha,
                        minLength: minLength(2),
                    },
                    surname: {
                        required,
                        alpha,
                        minLength: minLength(2),
                    },
                    street: {
                        required,
                        minLength: minLength(3),
                    },
                    house: {
                        required
                    },
                    flat: {
                        required,
                        numeric
                    },
                    phone: {
                        required,
                        nineDigitValidator: function (value) {
                            return value.length === 9 && _.every(value, (v) => _.isNumber(v * 1));
                        }
                    },
                    email: {
                        required,
                        email
                    }
                }
            }
        }
        ,
        mounted() {
            this.reloadImage()
        },
        watch: {
            imgUrl: {
                handler: function (newVal, oldVal) {
                    if (!newVal) {
                        newVal = oldVal
                    }
                },
                deep: true
            }
        },
        methods: {
            slide: function (page) {
                let margin = -400 * page;
                this.pageMarginStyle = `margin-left: ${margin}px;`;
                this.page = page;
            },
            selectPosition: function (positionId) {
                if (_.contains(this.selectedPositions, positionId)) {
                    this.selectedPositions = _.filter(this.selectedPositions, function (p) {
                        return p !== positionId
                    })
                } else {
                    this.selectedPositions.push(positionId);
                }
            },
            reloadImage: function () {
                fetch("https://picsum.photos/150", {method: 'GET'})
                    .then((response) => {
                        this.imgUrl = {id: _.uniqueId() * 1, url: response.url};
                        this.selectedImages.push(this.imgUrl);
                    })
            },
            setPreviousImage: function () {
                if (this.previousImageAvailable()) {
                    this.imgUrl = _.findWhere(this.selectedImages, {id: this.imgUrl.id - 1});
                }
            },
            setNextImage: function () {
                if (this.nextImageAvailable()) {
                    this.imgUrl = _.findWhere(this.selectedImages, {id: this.imgUrl.id + 1});
                }

            },
            previousImageAvailable: function () {
                return _.any(this.selectedImages, (img) => {
                    if (!img) {
                        return false;
                    }
                    return img.id < this.imgUrl.id;
                })
            },
            nextImageAvailable: function () {
                return _.any(this.selectedImages, (img) => {
                    if (!img) {
                        return false;
                    }

                    return img.id > this.imgUrl.id;
                })
            },
            order: function () {
                const order = {
                    tshirt: {
                        printSide: this.selectedPositions,
                        imgUrl: this.imgUrl.url,
                        price: this.price
                    },
                    user: {
                        name: this.user.name,
                        surname: this.user.surname,
                        adress: {
                            street: this.user.street,
                            house: this.user.house,
                            flat: this.user.flat
                        },
                        contacts: {
                            phone: this.user.phone,
                            email: this.user.email
                        }
                    }
                }
                console.log(order)
                this.slide(4);
            }
        }
    }
</script>

<style scoped>
    #orderForm {
        justify-content: center;
        background: white;
    }

    .container {
        display: inline-block;
        width: 400px;
        height: 200px;
        background: #DDDDF0;
        border-radius: 5px;
        text-align: center;
        padding: 20px 0px 45px 70px;
        overflow: hidden;
    }

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

    .form-outer form .page .field input {
        height: 100%;
        width: 100%;
        border: 1px solid lightgrey;
        border-radius: 5px;
        font-size: 10px;
        padding-left: 5px;
    }

    .form-outer form .page .field button {
        width: 100%;
        height: calc(100% + 5px);
        border: none;
        border-radius: 5px;
        background: #403D75;
        color: #fff;
        font-size: 13px;
        font-weight: 600;
        letter-spacing: 1px;
        text-transform: uppercase;
        cursor: pointer;
        margin-right: 2px;
        margin-left: 2px;
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


    form .page .btns button:disabled {
        margin-right: 3px;
        font-size: 17px;
        background: #ccc;
    }


    .container .progress-bar {
        display: flex;
        height: 60px;
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

    .form-group--error input {
        border-color: red !important;
        background: #FDD;
    }

    .error {
        outline-color: #F99;
    }

    .confirmation {
        height: 120px;
    }

    .confirmationSection {
        margin-top: 20px;
        text-align: initial;
        width: 85%;
        font-size: 14px;
    }

    .leftFloat {
        float: left;
        clear: both;
    }

    .rightFloat {
        float: right;
    }

    .lowercase {
        text-transform: lowercase;
    }

    .orderConfirmation {
        width: 95%;
        font-size: 14px;
    }

    .orderConfirmation th {
        text-align: left;
    }

    .orderConfirmation td {
        text-align: right;
    }

    .ellipse {
        width: 720px;
        height: auto;;
        background: #DDDDF0;
        border-radius: 200px
    }

    .center {
        display: flex;
        justify-content: center
    }

</style>
