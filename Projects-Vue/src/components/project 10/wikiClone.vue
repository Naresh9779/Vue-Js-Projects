<script setup>

import {ref} from 'vue';
const searchQuery=ref('');
const searchResult=ref([]);
const error=ref(null);
const isLoading=ref(false);

const searchWiki=async (query)=>{

const encodedQuery=encodeURIComponent(query);
const endPoint=`https://en.wikipedia.org/w/api.php?action=query&list=search&srsearch=${encodedQuery}&format=json&origin=*`;
try{
       isLoading.value=true;
    const response=await fetch(endPoint);
    const data=await response.json();
    console.log(data.query.search);

    if(data.query&&data.query.search.length>0)
    {

        
        searchResult.value=data.query.search;
        error.value=null;
     
        console.log(searchResult.value);
    }
  
    else{
        error.value='* No Result Found';
        searchResult.value=[];
        console.log(error.value);
       
    }
   
}catch(e) {
    console.log(`Error: ${e.message}`);
    error.value='* Error While Searching';
    searchResult.value=[];



}
finally{
    isLoading.value=false;

}




}

const sumbitSearch=()=>{
    if(searchQuery.value.trim()!='')
    {
        searchWiki(searchQuery.value);
    }
    else{
        searchResult.value=[];
        error.value='* Please Enter Something';
        console.log(error.value);
    }
}



</script>



<template>
   <div class="main">
    <div class="container">
        
            <div class="heading">
                <h1>Search Wikipedia</h1>
            </div>

            <div class="search-box">
                <input type="text" v-model="searchQuery" @keyup.enter="sumbitSearch" placeholder="Search Wikipedia">
                <a @click="sumbitSearch" class="search-btn">Search</a>
            </div>

            <div class="result-box">
                <div class="spinner" v-if="isLoading"></div>
                <p v-if="!isLoading" class="error">{{ error }}</p>
             
               <p v-if="searchResult.length" class="result-card">
                <div class="search-result " v-for="result in searchResult" :key="result.pageid"  >
                  
                  
                    <a :href="`https://en.wikipedia.org/?curid=${result.pageid}` " class="title-link" target="_blank"><h3>{{ result.title }}</h3></a>
                    <p v-html="result.snippet"></p>
                    <a :href="`https://en.wikipedia.org/?curid=${result.pageid} `" class="snippet" target="_blank">{{ `https://en.wikipedia.org/?curid=${result.pageid}` }}</a>
                 


                </div>
                  
            </p>
            </div>








    </div>
</div> 
</template>



<style>
@import url('https://fonts.googleapis.com/css2?family=Montserrat:ital,wght@0,100..900;1,100..900&display=swap');

*{
    margin: 0;
    padding: 0;
}
html{
    font-family: "Montserrat", sans-serif;
  font-optical-sizing: auto;
  font-weight: 400;
  font-style: normal;

}
h1{
    font-size: 4rem;
}
h3{
    display: block;
}
a{
    display: inline-block;
}
.main{
    display: flex;
    justify-content: center;
}

.container{
    display :flex;
    /* justify-content:center; */
    align-items: center;
    /* border:2px solid black; */
    flex-direction: column;
    margin-top: 0.5rem;
    padding-top:2rem ;
    gap:2rem;

    /* height: 100vh; */
    width:50vw
}
.result-box{
    margin-top: -1.8rem;
    /* border: 2px solid red; */
   display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    /* gap:3rem; */
    
   
}
.search-box{
    display: flex;
    gap: 1rem;
    align-items: center;
}
.snippet{
    color: rgb(3, 101, 3);
    font-size: 0.8rem;
}
.result-card{
    
    display: flex;
    width:70vw;
    flex-direction: column;
    gap: .2rem;
    /* box-shadow: 2px 2px 7px grey; */
    margin-top: 1rem;
    /* margin-bottom: 1rem; */
 
}
.search-btn{
    text-align: center;
    background-color:black ;
    color: white;
    border-radius: 2rem;
    padding: .7rem;
}
.search-btn:hover{
    background-color: rgb(42, 38, 253);
    cursor: pointer;
}

.search-result{
  
    width:60%;
    margin:auto;
    display: grid;
    grid-template-rows: 1fr 2fr 1fr;
    /* row-gap: 1rem; */
    /* border: 2px solid black; */
    box-shadow: 2px 2px 7px grey;
    
    border-radius: .8rem;
    padding: .8rem;
  

}

a{
    text-decoration: none;
}

input{
    border: 2px solid black;
    padding: .7rem;
    border-radius: 21px;
    font-size: 1rem;
}


.spinner{
   
    border:5px solid white;
    /* background-color:purple; */
    height:25px;
    width:25px;
    border-top: 5px solid rgb(42, 38, 253);
    border-radius: 50%;
    animation: spin 1s infinite linear ;
}
@keyframes spin {
    to{
        transform: rotate(360deg);
    }
    
}
.error{
    font-size: .6rem;
    font-weight: bolder;
color:red;
   /* border: 2px solid black; */
   /* width:100%; */

margin-right:7rem ;
 

}
.title-link:hover{
     
     cursor: pointer;
     text-decoration: underline;
     font-size: 1.1rem;
    
}
@media (max-width:431px){
.result-card{
    width: 129vw;
  
}
p{
    font-size: 1rem;
}


}

</style>