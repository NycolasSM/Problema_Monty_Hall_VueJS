<template>
    <div id="app">
        <h1>Problema de Monty Hall</h1>
        <div class="form">
            <div v-if="!started">
                <label for="portsAmount">Quantas portas?</label>
                <input type="text" id="portsAmount" size="3" v-model.number="portsAmount">
            </div>
            <div v-if="!started">
                <label for="selectedPort">Qual porta é premiada?</label>
                <input type="text" id="selectedPort" size="3" v-model.number="selectedPort">
            </div>
            <button v-if="!started" @click="started = true">Iniciar</button>
            <button v-if="started" @click="started = false">Reiniciar</button>
        </div>
        <div class="doors" v-if="started">
            <div v-for="i in portsAmount" :key="i">
                <Door :hasGift="i === selectedPort" :number="i" />
            </div>
        </div>
        <Instructions v-if="started" class="instrucoes"/>
    </div>
</template>

<script>
import Door from './components/Door'
import Instructions from './components/Instructions.vue'

export default {
    name: 'App',
    components: { Door, Instructions },
    data: function() {
        return {
            started: false,
            portsAmount: 3,
            selectedPort: null
        }
    }
}
</script>

<style>
* {
    box-sizing: border-box;
    font-family: 'Montserrat', sans-serif;
}

body {
    color: #fff;
    background: linear-gradient(to right, rgb(21, 153, 87), rgb(21, 87, 153))
}

#app {
    display: flex;
    flex-direction: column;
    align-items: center;
}

#app h1 {
    border: 1px solid #000;
    background-color: #0004;
    padding: 20px;
    margin-bottom: 60px;
}

.form {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    margin-bottom: 40px;
}

.form, .form input, .form button {
    margin-bottom: 10px;
    font-size: 1.4rem;
}

.doors {
    align-self: stretch;
    display: flex;
    justify-content: space-around;
    flex-wrap: wrap;
}

.instrucoes {
    border: 1px solid #000;
    background-color: #0004;
    padding: 20px;
    position: absolute;
    right: 5px;
    height: 180px;
    width: 250px;
}

.instrucoes h2 {
    font-size: 18px;
    margin: 0;
    display: flex;
    justify-content: center;
    align-items: center;
}

.instrucoes p {
    font-size: 15px;
}

.form input {
    margin-left: 10px;
    width: 55px;
    text-align: center;
}

</style>