<template>
<div class="page">
    <div class="logoContainer">
        <img class="logo" src="../assets/logo.png" alt="logo"/>
    </div>
    <div class="inputContainer">
        <div>
            <input type="text" v-model="height" @keypress="isNumber" placeholder="enter your height in meters" class="inputBox">
        </div>
        <div>
            <input type="text" v-model="weight" @keypress="isNumber" placeholder="enter your weight in kg" class="inputBox">
        </div>
    </div>
    <div class="btnContainer">
        <button @click="clickFn" class="button">
            generate
        </button>
    </div>
</div>
</template>

<script>
import { ref } from 'vue';

const height = ref();
const weight = ref();

export default{
    setup(){
        function BmiCalculation(){
            let BMI = 0;
            BMI = Math.round(Number(weight.value) / (Number(height.value) * Number(height.value)));
            let result = isNaN(BMI) ? "enter a proper value" : BMI;
            this.$store.state.counter = result;
        }
        return{
            height,
            weight,
            BmiCalculation
        }
    },
   methods:{
    clickFn(){
        if((height.value) === undefined || weight.value === undefined){
            alert('enter the input fields to proceed further')
        }else{
            this.$router.push('/result');
            this.BmiCalculation();
        }
    },
    isNumber(e){
        let char = String.fromCharCode(e.keyCode);
        /^\d*\.?\d*$/gm.test(char) ? true : e.preventDefault();
    }
   },
}
</script>

<style scoped>

.inputContainer{
    display: flex;
    flex-direction: column;
    justify-content: center;
    width: 100%;
}

.inputBox{
    margin: 20px;
    width: 50%;
    height: 30px;
    border: 0px;
    max-width: 500px !important;
    min-width: 200px !important;
}

.btnContainer{
    width: 100%;
}

.button {
    margin: 20px;
    justify-content:center;
    width: 50%;
    height: 30px;
    max-width: 500px !important;
    min-width: 200px !important;
    transition-duration: 0.4s;
    font-size: 80%;
}

.button:hover{
    background-color: #4CAF50; /* Green */
    color: white;
}
.logo{
    justify-content: center;
}
</style>