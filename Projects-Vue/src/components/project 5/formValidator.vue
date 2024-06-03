<script setup>

import {ref,computed} from 'vue';

const formData=ref({
    name:'',
    email:'',
    password:''
})
const isValidName=computed(()=>formData.value.name.trim()!='');

const isValidEmail=computed(()=> /\S+@\S+\.\S+/.test(formData.value.email));
const isValidPassword=computed(()=> formData.value.password.length>8);

const isFormValid=computed(()=> isValidName.value && isValidPassword.value && isValidEmail.value);
console.log(isFormValid.value);

const sumbitForm=()=>{
    if(isFormValid.value)
    {
        console.log('Form Submitted');
        alert("Form Submitted");
    }

    else
    {
        console.log('Form Invalid');
        alert("Form Invalid");
    }

}


</script>

<template>
   <form @submit.prevent="sumbitForm" class="form-group">
    <div class="form-div">
        <label>Name</label>
        <input v-model="formData.name" type="name" placeholder="Enter Ur Name">
        <span v-if="!isValidName" >*Enter Valid Name</span>
    </div>
    <div class="form-div">
        <label>Email</label>
        <input v-model="formData.email"  type="name" placeholder="Enter Ur Email">
        <span v-if="!isValidEmail" class="div-span">*Enter Valid Email</span>
    </div>

    <div class="form-div" id="form-pass">
        <label >Password</label>
        <input class="passin" v-model="formData.password" type="name" placeholder="Enter Ur password">
        <span class="span-pass" v-if="!isValidPassword">*Enter A Password More Than 8 Character</span>
    </div>

    <button  type="sumbit" >Sumbit Form</button>
</form>

</template>

<style>

.form-group{
    background-color:aliceblue;
    border: 2px solid black;
    border-radius: 12px;
    width:33%;
    margin:auto;
    padding: 4px 4px;
   display: flex;

   flex-direction: column;
   /* align-items: center; */
  
   
    
}

input{
    
    
    margin :2px;
    width:90%;
    height:35px;
    border-radius: 12px;
    font-size: 15px;
 
}

span{
   
    color:red;
    font-size: 10px;
    font-weight: bolder;
   

}

.form-div{
    display: flex;
    flex-direction: column;
 


padding: 10px;
display: flex;
}

label{
    font-family: Georgia, 'Times New Roman', Times, serif;
   font-size: 20px;
}
button{
    background-color: white;
    width: fit-content;
    padding: 10px;
    margin-left:3px;
    border-radius: 12px ;
}

button:hover{
    background-color: rgb(58, 183, 58);
}

</style>