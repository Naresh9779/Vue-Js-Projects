<script setup>

import {ref,onMounted} from 'vue';

const quotes = ref([
  {
    quote: "The only way to do great work is to love what you do.",
    author: "Steve Jobs"
  },
  {
    quote: "In the end, it's not the years in your life that count. It's the life in your years.",
    author: "Abraham Lincoln"
  },
  {
    quote: "Life is what happens when you're busy making other plans.",
    author: "John Lennon"
  },
  {
    quote: "Success is not final, failure is not fatal: It is the courage to continue that counts.",
    author: "Winston Churchill"
  },
  {
    quote: "The greatest glory in living lies not in never falling, but in rising every time we fall.",
    author: "Nelson Mandela"
  }
]);
const currentQuote=ref({quote:'',author:''})

const randomQuote=()=>{
    const randomIndex=Math.floor(Math.random()*quotes.value.length)
    currentQuote.value=quotes.value[randomIndex];
}

onMounted(randomQuote);



</script>
<template>

<div class="container">

    <h1>Random Quote Generator</h1>
<blockquote>
    <p>{{currentQuote.quote}}</p>
    <p>~~{{currentQuote.author}}</p>
</blockquote>
    <button @click="randomQuote">New Quote</button>



</div>


</template>

<style>
h1{
    margin :0 160px
}
.container {

    border: 2px solid black;
    display: inline-block;
    padding: 8px 3px;
    margin: 70px 395px;
}

blockquote{
    font-style: italic;
    font-size: 20px;
    font-weight: bold;
    border: 2px solid whitesmoke;
    padding: 3px 10px;
    background-color: aliceblue;
    
}

button{
    
    background-color: rgb(53 233 111);
    border: 2px solid #d9bebe;
    margin: 15px 201px;
    border-radius: 4px;
    padding: 4px 56px;
    font-size: 20px;
    font-weight: bold;
    font-family:'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
}



</style>