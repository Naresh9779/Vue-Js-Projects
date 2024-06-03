<script setup>

import { ref } from 'vue';

const steps=ref(['Step 1','Step 2','Step 3']);
const currentStep=ref(0);

const nextStep=()=>{
    if(currentStep.value<steps.value.length)
    {
        currentStep.value++;
        console.log(currentStep.value);
    }
}

const prevStep=()=>{
    if(currentStep.value>0)
    {
        currentStep.value--;
    }
}





</script>

<template>
    <div class="container">
        <div :class="{'step-box':currentStep==index}" v-for="(step,index) in steps ":key="index">
        
        {{ step }}</div>
       
        <button id="b1" @click="prevStep" :disabled="currentStep==0">Prev</button>
    <button id="b2" @click="nextStep" :disabled="currentStep==steps.length-1">Next</button>
    </div>





</template>


<style>

.container {

    /* border: 2px solid red; */
    width:33%;
    margin :auto;

    display: flex;
    align-items: center;
   
}
div div{
    
    /* border: 2px solid black; */
    padding: 20px 20px;

}
.step-box{
    background-color: rgb(28, 181, 28);

}

button:disabled{
    background-color: rgb(255, 255, 255);
}


button{
    background-color: rgb(28, 181, 28);
    color: white;
    padding: 10px 20px;
    border-radius: 10px;
    border: none;
    margin: 10px;
    cursor: pointer;
    /* position: absolute; */
    /* bottom:20px; */
}





</style>