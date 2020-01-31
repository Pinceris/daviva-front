<template>
    <div class="container">
        <section v-if="infoList.length > 0" class="custom-control-inline">
        <div v-for="(info, index) in infoList" :key="index" class="card" style="width: 18rem; margin-left: 10px">
            <img :src="info.nuotrauka" class="card-img-top" alt="nuotraukos nera">
            <div class="card-body" style="text-align: left">
                <h5 class="card-title">{{info.marke}}</h5>
                <p class="card-text">
                    Modelis: {{info.modelis}} <br>
                    Metai: {{info.metai}}
                </p>
                <a class="kaina">Kaina: {{info.kaina}}€</a>
            </div>
            <button class="arrow left" v-on:click="changePicture(index,false, info)">&#8249;</button>
            <button class="arrow right" v-on:click="changePicture(index,true, info)">&#8250;</button>
        </div>
        </section>
        <div>
            <button class="btn btn-primary" v-on:click="getCar">Prideti</button>
        </div>
    </div>
</template>

<script>
    import axios from 'axios'

    export default {
        name: 'Cars',
        data() {
            return {
                infoList: [],
                info: null,
                counters: []
            }
        },
        methods: {
            getCar() {
                axios
                    .get('https://backend.daviva.lt/API/InformacijaTestui')
                    .then(response => (this.info = response))
                    // eslint-disable-next-line no-console
                    .catch(error => console.log(error))
                    .finally(() => this.pushToList(this.info.data));
            },
            pushToList(info) {
                this.counters.push(0);
                let car = {
                    marke: info.marke,
                    modelis: info.modelis,
                    metai: info.metai,
                    nuotraukos: info.nuotraukos,
                    nuotrauka: info.nuotraukos[0],
                    kaina: info.kaina,
                };
                this.infoList.push(car);
            },
            changePicture(index, next, info) {
                if(next === true && this.counters[index] < 3)
                {
                    this.counters[index]++;
                    info.nuotrauka = info.nuotraukos[this.counters[index]];
                }
                else if(this.counters[index] > 0)
                {
                    this.counters[index]--;
                    info.nuotrauka = info.nuotraukos[this.counters[index]];
                }
            }
        }
    }
</script>

<style scoped>
    .container{
        width: 100%;
    }
    .custom-control-inline{
        margin-bottom: 10px;
    }
    .kaina{
        margin-left: 20px;
        padding: 10px 40px 10px 40px;
        background-color: darkgray;
        color: #42b983;
        border-radius: 25px;
    }
    .container {
        position: relative;
        width: 50%;
    }

    /* Make the image responsive */
    .card img {
        width: 100%;
        height: auto;
    }

    /* Style the button and place it in the middle of the container/image */
    .card .left {
        position: absolute;
        top: 30%;
        left: 2%;
        transform: translate(-50%, -50%);
        -ms-transform: translate(-50%, -50%);
        background-color: #555;
        color: white;
        font-size: 16px;
        padding: 12px 6px;
        border: none;
        cursor: pointer;
        border-radius: 5px;
    }
    .card .right {
        position: absolute;
        top: 30%;
        left: 98%;
        transform: translate(-50%, -50%);
        -ms-transform: translate(-50%, -50%);
        background-color: #555;
        color: white;
        font-size: 16px;
        padding: 12px 6px;
        border: none;
        cursor: pointer;
        border-radius: 5px;
    }
</style>