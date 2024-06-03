<script setup>

import {ref} from 'vue'
const  newtask=ref('')
const tasks=ref([])

const addTask=()=>{
    if(newtask.value.trim()!='')
    {
        tasks.value.push(newtask.value)
        newtask.value=''
    }

}


const removeTask=(index)=>{
    tasks.value.splice(index,1)
}
</script>

<template>
 <div class="todo-app">
     <h1 class="title">To Do List</h1>
     <div class="task-input">
     <input type="text" placeholder="Enter You Task" v-model="newtask" @keyup.enter="addTask">
     <button @click="addTask">Add Task</button>
 </div>
     <ul class="taskList">
        <li v-for="(task,index) in tasks" class="task-item">{{ task }}
            <button @click="removeTask(index)" class="remove-button">Remove</button>
        </li>
       

     </ul>



 </div>
</template>

<style>
.todo-app{
   max-width: 400px;
   margin :50px auto;
   padding: 20px;
   border: solid 2px black;
   border-radius: 8px;
   box-shadow: 0 2px 4px aquamarine;
   
}
.title{
    text-align: center;
    
    font-size: 24px;
    margin-bottom: 20px;
}
.task-input{


    display: flex;
    gap:10px;
}
input{

   flex:1;
   padding: 8px;

   font-size: 14px;
}

button{
    padding: 8px 12px;
    font-size: 14px;
    background-color: rgb(91, 255, 91);
    color: #fff;
    border:none;
    border-radius: 4px;
    cursor: pointer;
}
button:hover{
    background-color: rgb(7, 8, 7);

}

.tasklist{
    list-style: none;
    padding: 0;
}
.task-item{
   display: flex;
   justify-content: space-between;
   align-items: center;
   padding: 10px;
   margin: 8px 0;
   background-color: #f9f9f9;
   border: 1px solid #e6e6e6;
   border-radius: 4px;
}

.remove-button{
     padding: 6px 10px;
     font-size: 12px;
    background-color: red;
    
    color:white;
    border:none;
    border-radius: 3px;
}





</style>