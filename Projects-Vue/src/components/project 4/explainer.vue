<script setup>

import {ref} from 'vue';

const items =ref(
[
    {
        title: "Lorem Ipsum",
        description: "Lorem ipsum dolor sit amet, consectetur adipiscing elit.",
        open: false
    },
    {
        title: "Random Data",
        description: "Generating random data for JSON examples.",
        open: false
    },
    {
        title: "Sample Title",
        description: "This is just a sample description.",
        open: false
    },
    {
        title: "Test Item",
        description: "This is a test item for JSON data generation.",
        open: false
    }
]

)

const toogleItem=(index)=>{
   
    items.value=items.value.map((item,i)=>(
        {

        ...item,
        
        open:i==index?!item.open:false
    })
)



}



</script>

<template>
    
  <div class="container">
    <div v-for="(item,i) in items":key="i" class ="explainer-content">
       <div @click="toogleItem(i)" class="title">{{ item.title }}
    <div class="arrow">{{ item.open?"⬇️" :"➡️"}}</div>
     </div>

     <div v-show="item.open" class="description">{{ item.description,console.log(item.description) }}
    </div>
    </div>
</div>






</template>
<style>

.container{
    border:2px solid black;
    display :flex;
    flex-direction:column;
    align-items:center;

   
}
.explainer-content{
    border:2px solid black; 
    width :33%;
    margin :14px;
  
    padding: 14px 6px;
   
    background-color:darkblue;
}
.title{
    font-weight: bold;
    color: antiquewhite;
    margin :0px 19px;
    padding-top:2px;
    cursor: pointer;
}
.arrow{
    /* position: absolute; */
    /* display: inline; */
     /* right:310px;
    top:40px;  */
}
.description{
    background-color: aliceblue;
    padding: 14px 6px;
}

</style>
