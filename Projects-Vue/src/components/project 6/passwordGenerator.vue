<script setup>
import {ref} from 'vue'

const passwordLength=ref(12)
const includeLowerCase=ref(true)
const includeUpperCase=ref(true)
const includeSymbols=ref(true)
const generatedPassword=ref('')

const generatePassword=()=>{
    console.log(`Generating password.......`);
    
    const lowerCase=includeLowerCase.value?'abcdefghijklmnopqrstuvwxyz':'';
    const upperCase=includeUpperCase.value?'ABCDEFGHIJKLMNOPQRSTUVWXYZ':'';
    const symbols=includeSymbols.value?'~!@#$%^&*()_+{}|:"<>?':'';
    
    const allChars=lowerCase+upperCase+symbols;
    console.log(allChars);
    let password='';
    // consol
    for(let i=0; i<passwordLength.value; i++)
    {
        const randomChar=allChars[Math.floor(Math.random()*allChars.length)];
        console.log(randomChar);
         password=password+randomChar;
        
    }
   
    generatedPassword.value=password;
   
}









</script>
<template>
   <div class="container">
    <h1>Password Generated</h1>

    <label>Include LowerCase : </label>
    <input type="checkbox" name="IncludeLowercase" v-model="includeLowerCase">
  
    <label>Include LowerCase : </label>
    <input type="checkbox" name="IncludeUpperCase" v-model="includeUpperCase">

    <label>Include Symbols :</label>
    <input type="checkbox" name="IncludeSymbols" v-model="includeSymbols">
   
    <button @click="generatePassword">Generate Password </button>
   
    <strong>Generated Password is : {{ generatedPassword }}</strong>
</div>
</template>
<style>

.container{
    border: 2px solid black;
    width :33%;
    margin: auto;
    display: flex;
    flex-direction: column;
}
button {
    margin-top: 10px;
    margin-bottom: 10px;
    padding: 10px;
    border: 2px solid black;
    border-radius: 10px;
    background-color: rgb(255, 255, 255);
    color: rgb(0, 0, 0);
    font-size: 15px;
    font-weight: bold;
    cursor: pointer;
    width:60%;
    margin: auto;
}
button:hover{
    background-color: rgb(32, 138, 32);
}
h1{
    width:60%;
    margin: auto;
}
</style>