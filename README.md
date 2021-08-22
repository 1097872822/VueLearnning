+ ## 声明式编码

  ![image-20210822132201405](https://blogrrw.oss-cn-shenzhen.aliyuncs.com/bloguse/20210822214346.png)

  + 初识vue.html

    + Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。

      ```html
      <!-- 准备好一个容器 -->
      <div id="demo">
      	<h1>Hello，{{name.toUpperCase()}}，{{address}}</h1>
      </div>
      
      //创建Vue实例
      new Vue({
      	el:'#demo', //el用于指定当前Vue实例为哪个容器服务，值通常为css选择器字符串。
      	data:{ //data中用于存储数据，数据供el所指定的容器去使用，值我们暂时先写成一个对象。
      		name:'atguigu',
      		address:'北京'
      	}
      })
      ```

  + ##### 模板语法：

    + ###### 指令语法：

      ```html
      <a v-bind:href="school.url.toUpperCase()" x="hello">点我去{{school.name}}学习1</a>
      <a :href="school.url" x="hello">点我去{{school.name}}学习2</a>
      
      data:{
      	name:'jack',
      	school:{
      	name:'尚硅谷',
      	url:'http://www.atguigu.com',	
      }
      		功能：用于解析标签（包括：标签属性、标签体内容、绑定事件.....）。
      		举例：v-bind:href="xxx" 或  简写为 :href="xxx"，xxx同样要写js表达式，									 且可以直接读取到data中的所有属性。
      		备注：Vue中有很多的指令，且形式都是：v-????，此处我们只是拿v-bind举个例子。
      ```

      功能：用于解析标签（包括：标签属性、标签体内容、绑定事件.....）。

      举例：v-bind:href="xxx" 或 简写为 :href="xxx"，xxx同样要写js表达式，

      ​                   且可以直接读取到data中的所有属性。

      备注：Vue中有很多的指令，且形式都是：v-????，此处我们只是拿v-bind举个例子。

  + ##### 数据绑定

    + 1.单向绑定(v-bind)：数据只能从data流向页面。

    + 2.双向绑定(v-model)：数据不仅能从data流向页面，还可以从页面流向data。

      + 备注：

        1.双向绑定一般都应用在表单类元素上（如：input、select等）

      ​       2.v-model:value 可以简写为 v-model，因为v-model默认收集的就是value值。

  + #### el 与 data

    + ###### data与el的2种写法

      + 1.el有2种写法

      ​       (1).new Vue时候配置el属性。

      ​       (2).先创建Vue实例，随后再通过vm.$mount('#root')指定el的值。

      + 2.data有2种写法

      ​         (1).对象式

      ​         (2).函数式

      ​         如何选择：目前哪种写法都可以，以后学习到组件时，data必须使用函数式，否则会报错。

      + 3.一个重要的原则：

      ​         由Vue管理的函数，一定不要写箭头函数，一旦写了箭头函数，this就不再是Vue实例了。

  + #### 数据代理[Object.defineProperty]

    ![image-20210822155813235](https://blogrrw.oss-cn-shenzhen.aliyuncs.com/bloguse/20210822214342.png)

    ###### 1.Vue中的数据代理：通过vm对象来代理data对象中属性的操作（读/写）

    2.Vue中数据代理的好处：更加方便的操作data中的数据

    3.基本原理：

    ​	通过Object.defineProperty()把data对象中所有属性添加到vm上。

    ​    为每一个添加到vm上的属性，都指定一个getter/setter。

    ​    在getter/setter内部去操作（读/写）data中对应的属性。

  + #### 事件的基本使用

    + 1.使用v-on:xxx 或 @xxx 绑定事件，其中xxx是事件名；
    + 2.事件的回调需要配置在methods对象中，最终会在vm上；
    + 3.methods中配置的函数，不要用箭头函数！否则this就不是vm了；
    + 4.methods中配置的函数，都是被Vue所管理的函数，this的指向是vm 或 组件实例对象；
    + 5.@click="demo" 和 @click="demo($event)" 效果一致，但后者可以传参；
      + Vue中的事件修饰符：
        + 1.prevent：阻止默认事件（常用）；
        + 2.stop：阻止事件冒泡（常用）；
        + 3.once：事件只触发一次（常用）；
        + 4.capture：使用事件的捕获模式；
        + 5.self：只有event.target是当前操作的元素时才触发事件；
        + 6.passive：事件的默认行为立即执行，无需等待事件回调执行完毕；

  + ##### 计算属性

    + 1.定义：要用的属性不存在，要通过已有属性计算得来。
    + 2.原理：底层借助了Objcet.defineproperty方法提供的getter和setter。
    + 3.get函数什么时候执行？
      + (1).初次读取时会执行一次。
      + (2).当依赖的数据发生改变时会被再次调用。
    + 4.优势：与methods实现相比，内部有缓存机制（复用），效率更高，调试方便。
    + 5.备注：

    ​       1.计算属性最终会出现在vm上，直接读取使用即可。

    ​       2.如果计算属性要被修改，那必须写set函数去响应修改，且set中要引起计算时依赖的数据发生改变。 


