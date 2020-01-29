<template>
    <div class="container">
        <section v-if="infoList.length > 0" class="custom-control-inline">
        <div v-for="info in infoList" :key="info.modelis" class="card" style="width: 18rem; margin-left: 10px">
            <img :src="info.nuotraukos[0]" class="card-img-top" alt="nuotraukos nera">
            <div class="card-body" style="text-align: left">
                <h5 class="card-title">{{info.marke}}</h5>
                <p class="card-text">
                    Modelis: {{info.modelis}} <br>
                    Metai: {{info.metai}}
                </p>
                <a class="kaina">Kaina: {{info.kaina}}€</a>
            </div>
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
                info: null
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
                let car = {
                    marke: info.marke,
                    modelis: info.modelis,
                    metai: info.metai,
                    nuotraukos: info.nuotraukos,
                    kaina: info.kaina,
                };
                this.infoList.push(car);
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
</style>