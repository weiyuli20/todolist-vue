<script setup>
import { ref } from 'vue'
import axios from 'axios'
import HelloWorld from './components/HelloWorld.vue'
import TheWelcome from './components/TheWelcome.vue'


getList()
const list = ref([])
const str = ref('')


async function getList() {
  const res =  await axios({
  url: 'https://p181f90pve.hzh.sealos.run/getList',
  method: 'get',
})
list.value = res.data.data

console.log(list.value)

}


async function add(){
  const res = await axios({
    url: 'https://p181f90pve.hzh.sealos.run/add_todo',
    method: 'post',
    data: {
      text: str.value,
      is_completed: false
    }
  })
  await getList()
  console.log(res.data)
  str.value = ''
}

async function update(index){
  console.log(index)
  const res = await axios({
    url: 'https://p181f90pve.hzh.sealos.run/update',
    method: 'get',
    params: {
      id: index,
    }
  })
  await getList()
  console.log(res.data)
}

async function del(index){
  const res = await axios({
    url: 'https://p181f90pve.hzh.sealos.run/del',
    method: 'get',
    params: {
      id: index,
    }
  })
  // 从index 开始删除一个元素
  await getList()
  console.log(res.data)
}

</script>

<template>
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <div class="todo-app">
        <div class="title"> xx的Todo APP</div>
        <div class="todo-form">
            <input  v-model="str" type="text" class="todo-input" placeholder="add a to do">
            <div  @click="add" class="todo-button">Add todo</div>
        </div>

        <div  v-for="(item,index) in list" :class = "[item.is_completed ? 'completed' : 'item']">
            <div>
                <input @click="update(item._id)" v-model = "item.is_completed" type="checkbox">
                <span class="name">{{item.text}}</span>
            </div>
            
            <div  @click="del(item._id)" class ="del">del</div>
        </div>

       
        
        
    </div>
</body>

</template>

<style>
        .completed {
           display: flex;
            box-sizing: border-box;
            width: 80%;
            height: 50px;
            margin: 8px auto;
            padding: 16px;
            border-radius: 20px;
            box-shadow: rgba(149,157,165,0.2) 0px 8px 24px;
            justify-content: space-between;
            align-items: center;
            text-decoration: line-through;
            opacity: 0.5;
        }

        .del {
            color: red;
        }
        .item {
            display: flex;
            box-sizing: border-box;
            width: 80%;
            height: 50px;
            margin: 8px auto;
            padding: 16px;
            border-radius: 20px;
            box-shadow: rgba(149,157,165,0.2) 0px 8px 24px;
            justify-content: space-between;
            align-items: center;
        }

        .todo-input {
            border: 1px solid #dfe1e5;
            outline: none;
            width: 60%;
            height: 50px;
            border-radius: 20px 0 0 20px;
            padding-left: 15px;
            margin-bottom: 20px;
        }

        .todo-button {
            outline: none;
            width: 100px;
            height: 52px;
            border-radius:  0 20px 20px 0;
            color: #ffff;
            text-align: center;
            line-height: 52px;
            cursor: pointer;
            user-select: none;
        

            background: linear-gradient(
            to right,
            rgb(113,65,168),
            rgba(44, 114, 251,1)
            );

        }

        .todo-form {
            display: flex;
            margin-top: 20px;
            margin-left: 30px;
        }

        body {
        /* background: linear-gradient(to right, blue, purple); */
        background: linear-gradient(
            to right,
            rgb(113,65,168),
            rgba(44, 114, 251,1)
            );
        }
        .todo-app {
            margin-top: 40px;
            margin-left: 1%;
            width: 98%;
            height: 500px;
            background-color:#ffff;
            border-radius: 5px;
        }
        .title {
            font-size: 30px;
            font-weight: 700;
            text-align: center;
            padding-top: 30px;
            box-sizing: border-box;

        }
       
    </style>
