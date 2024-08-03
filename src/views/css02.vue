<template>
    <div class="container">
        <h1>Tip Calculator</h1>
        <p>Enter the bill amount and tip percentage to calculate the total.</p>
        <label for="bill">Bill amount:</label>
        <input type="number" id="bill" v-model="bill">
        <br />
        <label for="tip">Tip percentage:</label>
        <input type="number" id="tip" v-model="tip">
        <br />
        <button id="calculate" @click="Total">Calculate</button>
        <br />
        <label for="total">Total:</label>
        <span id="total">{{ total }}</span>
    </div>
</template>
<script setup>
import { ref } from 'vue'
const bill = ref('')
const tip = ref('')
const total = ref('')
function Total() {
    total.value = bill.value * (1 + tip.value / 100)
}

</script>
<style scoped>
* {
    box-sizing: border-box;
}

.container {
    background-color: white;
    color: black;
    max-width: 600px;
    margin: 100px auto;
    padding: 20px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.2);
    border-radius: 10px;
}

h1 {
    text-align: center;
    margin-top: 0;
}

input {
    padding: 10px;
    border: 1px solid #ccc;
    border-radius: 4px;
    margin: 10px 0;
    width: 100%;
}

button {
    background-color: #4caf50;
    color: white;
    padding: 10px;
    border: none;
    cursor: pointer;
    /* 鼠标点击时变为手型 */
    margin: 10px 0;
    width: 100%;
    font-size: 18px;
    text-transform: uppercase;
    transition: background-color 0.2s ease;
}

button:hover {
    background-color: #45a049;
}

#total {
    font-size: 24px;
    font-weight: bold;
    margin-top: 10px;
}
</style>