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