<script setup>
import {ref} from "vue";
import axios from 'axios';
const joke=ref(null)
const fetch=async()=>{
  try { 
    const response=await axios.get("https://icanhazdadjoke.com/",{
        headers:{
          "Accept":"application/json",
        }
        

    })
    // console.log(response)
        joke.value=response.data.joke;
}
  catch (error) {
    console.log("Error in Fetching Joke")
  }
  
}
</script>

<template>

    <div class="container">
         <div class="heading">
            <h1>Random Jokes 😆🤣</h1>
         </div>

         <div class="button">
            <button @click="fetch">Get Joke</button>
         </div>
         <div v-if="joke" class="joke">
            <p>{{joke}}</p>
         </div>
    </div>

</template>

<style>
*{
    padding: 0;
    margin: 0;
   
    color: aliceblue;
}
 .container{
    display:flex;
    flex-direction:column;
    /* justify-content:center; */
   
    align-items:center;
    height:55vh;
    width: 55vw;
    margin: auto;
    margin-top: 5rem;
    background-color: black;
    gap:2rem;
    border:2px solid white;
  }
 .heading{
    text-align:center;
    font-size:2rem;
    /* border: 2px solid white; */
  }
 button{
  
    margin-top:2rem;
      padding: 1rem;
      
      background-color: rgb(76, 76, 249);
      border-radius: 1rem;

  }
  button:hover{
    font-weight: bolder;
    background-color: rgb(53, 53, 251);

   
  }
 .joke{
    text-align:center;
    font-size:1.5rem;
    border: 2px solid white;
    margin: 1rem;
    padding: 1rem;
  }


</style>