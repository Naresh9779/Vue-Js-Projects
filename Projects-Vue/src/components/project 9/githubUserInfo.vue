<script setup>
import {ref} from 'vue';


const userName=ref('Naresh9779');
const error=ref(null);
const userProfile=ref(null);
const fetchData=async()=>{
    try{
    
        const response=await fetch(`https://api.github.com/users/${userName.value}`)
        const data= await response.json();
        
        if(response.ok)
        {
            userProfile.value=data;
            error.value=null;
        }

        else
        {
            error.value=`Error:${data.message}`;
            userProfile.value=null;
        }

    }catch(e)
    {
        console.log("Error In Getting Info",e.message);
        error.value=e.message;
    }
}

</script>

<template>
    <section>
    <div class="container">
        <h1>Github User Information</h1>
        <div class="search">


            <input type="text" v-model="userName">
            
            <a @click="fetchData" class="search-btn">Search</a>
        </div>

       <div class="section">
        <div v-if="error" class="error-msg">
            {{error}}
        </div>
        <div v-if="userProfile" class="user-card">
            
            <img :src="userProfile.avatar_url">
            <h1>{{userProfile.name}}</h1>
            <div class="follow-card">
                <p>Followers:{{ userProfile.followers }}</p>
                <p>Following:{{ userProfile.following }}</p>
            </div>
            <p><strong>Bio:</strong>{{userProfile.bio}}</p>
            <a :href="userProfile.html_url">Go TO Profile</a>
        </div>

    </div>
    </div>
</section>
</template>

<style>
section{
    display: flex;
    justify-content: center;
    align-items: center;
}
.follow-card{
    display: flex;
    justify-content: center;
    gap:1rem;
    font-weight: bold;
}
  .container{
    display:flex;
    justify-content:center;
    align-items:center;
    flex-direction:column;
    /* border:2px solid rgb(10, 10, 10); */
    padding: 2rem;
    margin-top: 1rem;
    /* box-shadow: 2px 2px 3px black; */
  
 
  }
  .follow-card:hover{
    color: blue;
    font-weight: bolder;
  }
  .user-card{
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    margin-top: 2rem;
    width:524px;
    height: 424px;

 
    padding: 1rem;
    /* border: 2px solid rgb(10, 10, 10); */
    box-shadow: 3px -3px 20px rgb(249, 194, 194);
    /* border-radius: 10px; */
  }
  img{
    margin-top: 2rem;
    width: 100px;
    height: 100px;
    border-radius: 10rem;
  }

  input{
    padding: 0.5rem;
    /* margin-top: 1rem; */
    /* border: 2px solid rgb(10, 10, 10); */
    /* box-shadow: 2px 2px 3px black; */
    border-radius: 10px;
  }
  .search{
    display: flex;
    gap: 1rem;



  }
  a{
    background-color: rgb(56, 198, 56);
    padding: 0.5rem;
    border-radius: 10rem;
    text-decoration: none;
    color: black;
  }
  a:hover{
    background-color: rgb(10, 10, 10);
    color: rgb(56, 198, 56);
    cursor: pointer;
  }

  
  p{
    width: 47%;
  }


</style>