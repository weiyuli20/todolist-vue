# todolist-vue

This template should help get you started developing with Vue 3 in Vite.

## Recommended IDE Setup

[VSCode](https://code.visualstudio.com/) + [Volar](https://marketplace.visualstudio.com/items?itemName=Vue.volar) (and disable Vetur).

## Customize configuration

See [Vite Configuration Reference](https://vite.dev/config/).

## Project Setup

```sh
npm install
```

### Compile and Hot-Reload for Development

```sh
npm run dev
```

### Compile and Minify for Production

```sh
npm run build
```

一个.vue 文件就是一个组件,一个组件由3部分构成：script, template, style,   script: 组件的逻辑代码 js，template: 组件的模板,html，style: 组件的样式

vue3中定义变量，使用ref
```
const name = ref('1234')
const age = ref(18)
conset user = ref({
    name: '123',
    age: 18
})
变量的使用：在script中str.value，在template中{{str}}
```

监听事件：
- 在script中定义函数

- @click="函数名"
- @mosueover="函数名"
- @mouseout="函数名"

双向绑定：输入框中的值实时地保存到变量中  v-model

```
const str1 =ref("")
function add(){
console.log(str1.value);

<input type="text" v-model="str1"/>
```

动态绑定
- 动态绑定类名：
    ```
    const str =ref(true)
    function add(){
    console.log(str.value);
    str.value = !str.value
    }

    样式使用str的值对应的类名
    <div :class="[str? 'completed','item']">
                <div>
                    <input v-model="str" type="checkbox">
                    <span class="name">吃饭</span>
                </div>
                
                <div class="del">del</div>
            </div>
    ```
- img 动态绑定src
  ```
  <img :src="img" alt="">
  ```
  
  - 列表渲染
  ```
    const list =ref(["吃饭","睡觉","打豆豆"])
    <div  v-for="(item,index) in list" class = "item">
            <div>
                <input  type="checkbox">
                <span class="name">{{item + index}}</span>
            </div>
            
            <div class="del">del</div>
    </div>

  ```

  - 侦听器：监听数据的变化
  ```
    const str = ref('')

    function change(){
    console.log(str.value)
    }

    watch(str,change)
    <input  v-model="str" type="text" >
  ```
  监听变化前后的值
  ```
    watch(str,(newValue,oldValue)=>{const str = ref('')

    function change(newValue,oldValue){
    console.log("新值："+newValue, "旧值："+oldValue)
    }

    watch(str,change)

  ```
  深度监听：当监听的数据为对象时，监听的对象的属性也会被监听
  ```
    const str = ref({
    text:""
    })

    function change(newValue,oldValue){
    console.log("新值："+newValue, "旧值："+oldValue)
    }

    watch(str,change,{deep:true})

    <input  v-model="str.text" type="text" >

  ```

- v-show 和v-if 控制页面是否显示
- v-show 是通过display:none;控制页面是否显示
- v-if 是直接不创建相关页面

- 组件：
  把可复用的页面封装成一个组件，组件可以复用，组件之间可以传递数据

  在vue中，所有以.vue结尾的文件都可以看做一个组件  一般组件放在components文件夹下，组件命名后缀为.vue

- 组件的使用:定义组件，在页面中导入组件，使用组件

  - 父组件数据传递给子组件：在子组件中调用 defineProps()
  ```
  Buutton.vue

  <script setup>
    import {defineProps} from 'vue'
    const props = defineProps(['text'])
    </script>

    <template>
        <div class='button'>{{props.text}}</div>
    </template>

    <style scoped>
    .button{
        width: 30px;
        height: 40px;
        background-color: #ffff;
        margin-top: 100px;
    }
    </style>
  ```
  ```
  父组件中
  import mybutton from './components/Button.vue'
  <mybutton text = "添加"></mybutton>
  <mybutton text = "删除"></mybutton>
  ```
  - 子组件向父组件传值
  ```
  <script setup>
    import {defineProps,defineEmits} from 'vue'

    const props = defineProps(['text'])
    // 'ok'是自定义事件名称
    const emit = defineEmits(['ok'])  

    function send(){
        emit('ok',"hello")
    }

    </script>

    <template>
        <div @click="send" class='button'>{{props.text}}</div>
        
    </template>

    <style scoped>
    .button{
        width: 30px;
        height: 40px;
        background-color: #ffff;
        margin-top: 100px;
    }

    </style>
    ```
    ```
    function print(str){
    console.log(str)
    }
    //监听ok时间
    <mybutton @ok ='print' text = "添加"></mybutton>
    ```
    点击添加按钮后会打印出hello

- axios 请求
  - 安装axios ```npm install axios```
  - 导入axios ```import axios from 'axios'```
  - 使用
    ```
    async function getList() {
        const res =  await axios({
        url: '/api/todo/list',
        method: 'get',
            })
        console.log(res)
        }
    ```
- 云开发平台 ：https://hzh.sealos.run/signin