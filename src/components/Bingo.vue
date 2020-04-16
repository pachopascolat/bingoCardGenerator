<template>
    <div class="div-bingo">
        <button v-on:click="createCartones">Crear</button>

        <div v-for="(cartones,key) in series" v-bind:key="key">
            <h3>Serie {{key+1}} </h3>
            <div class="div-cartones">

                <div v-for="(card,key) in cartones" v-bind:key="key">
                    <div class="card">
                        <div class="my-row" >
                            <div :class="(num===null?'my-null':'')"  class="my-col" v-for="num in card[0]" v-bind:key="num">
                                <div>{{num}}</div>
                            </div>
                        </div>
                        <div class="my-row" >
                            <div :class="(num===null?'my-null':'')"  class="my-col" v-for="num in card[1]" v-bind:key="num">
                                <div >{{num}}</div>
                            </div>
                        </div>
                        <div class="my-row" >
                            <div :class="(num===null?'my-null':'')"  class="my-col" v-for="num in card[2]" v-bind:key="num">
                                <div >{{num}}</div>
                            </div>
                        </div>

                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: "Bingo",
        data: function(){
            return {
                cardArray:[],
                tira:[[],[],[],[],[],[],[],[],[]],
                series:[],
            };
        },
        created() {
            this.createTira();
            // this.createCartones();

        },
        methods:{
            createCartones(){
                let cartones = [];
                this.createTira();
                let cards = this.createCard();
                cards = this.desordenarArray(cards);
                let i= 0;
                do{
                    cartones.push([cards[i],cards[i+1],cards[i+2]]);
                    i += 3;
                }while(i<18)
                this.series.push(cartones);

            },
            createTira(){
                let i = 1;
                while(i<=90){
                    if(i<10){
                        this.tira[0].push(i) ;
                    }else
                    if(i<20){
                        this.tira[1].push(i) ;
                    }else
                    if(i<30){
                        this.tira[2].push(i) ;
                    }else
                    if(i<40){
                        this.tira[3].push(i) ;
                    }else
                    if(i<50){
                        this.tira[4].push(i) ;
                    }else
                    if(i<60){
                        this.tira[5].push(i) ;
                    }else
                    if(i<70){
                        this.tira[6].push(i) ;
                    }else
                    if(i<80){
                        this.tira[7].push(i) ;
                    }else{
                        this.tira[8].push(i);
                    }
                    i++;
                }
            },
            desordenarArray(array){
                array.sort(function(){
                    return Math.random() - 0.5;
                });
                return array;
            },
            sortByLength(array){
                array = this.desordenarArray(array);
                array.sort(function (a, b) {
                    if (a.length > b.length) {
                        return -1;
                    }
                    if (a.length < b.length) {
                        return 1;
                    }
                    // a must be equal to b
                    return 0;
                });
                return array;
            },
            randomInt: function (min, max) {
                return Math.floor(Math.random() * (max - min) ) + min;
            },
            createCard: function(){
                let card = [];
                for(let j = 0 ; j < 18 ; j++) {
                    let row = [null,null,null,null,null,null,null,null,null];
                    this.sortByLength(this.tira);
                    for (let i = 0; i < 5; i++) {
                        let sacado = this.tira[i].splice(this.randomInt(0,this.tira[i].length-1),1)[0];
                        let col;
                        if(sacado==90){
                            col=8;
                        }else{
                            col = Math.trunc(sacado/10);
                        }
                        row[col] = sacado;
                    }
                    console.log(row);
                    card[j] = row;
                }
                return card;
            }
        }
    }
</script>

<style scoped>

    .my-row{
        display: flex;
    }
    .my-col{
        display: flex;
        justify-content: center;
        align-items: center;
        border: black 1px solid;
        /*flex: 1;*/
        width: 60px;
        height: 60px;
        font-size: 2em;
        /*padding: 4px;*/
    }
    .my-null{
        background-color: lightslategray;
    }
    .card{
        display: inline-block;
        border: black 1px solid;
        margin: 4px;
        /*width: 50%;*/
    }
    .div-cartones{
        display: flex;
        flex-wrap: wrap;
        justify-content: center;
        /*border: #2c3e50 1px solid;*/
    }

    .div-bingo{

    }
</style>
