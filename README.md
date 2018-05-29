# vue.js----set
vue.js中$set与数组更新



由于 JavaScript 的限制，Vue 不能检测以下变动的数组： 
当利用索引直接设置数组的某一项时，例如：vm.items[indexOfItem] = newValue 
当你修改数组的长度时，例如：vm.items.length = newLength，不会更新数组。 
当然vue中给了解决方法，就是使用 Vue.set, vm.$set(Vue.set的变种写法)或者 splice，caoncat等修改数组，同时也将触发状态更新： 


  
@@ 现在有两个数组，分别为arr1，arr2，如果arr1以下标赋值改变数组，arr2以$set改变数组，结果是什么样呢？  
  
  
          <div id="app">
            arr1
            <ul>
                <li v-for="arr1 in arr1">{{arr1}}</li>
            </ul>
            <br>
            
            arr2
            <ul>
                <li v-for="arr2 in arr2">{{arr2}}</li>
            </ul>
        </div>
  
  
          <script>
            var vm=new Vue({
                 el:"#app",
                data:{
                        arr1:['a','b','c'],
                        arr2:['foo','bar','baz']
                     }
                });
                 vm.arr1[1]='goods';  //如果没有vm.$set() arr1的数组是不会更新到视图的
                 vm.$set(vm.arr2,1,"77")   //  但是这里用vm.$set（） 更改arr2的数组 他会同时更新到视图上的
            </script>
  






             Vue.set() 响应式新增与修改数据

                  此时我们需要知道Vue.set()需要哪些参数，官方API：Vue.set()

                  调用方法：Vue.set( target, key, value )

                  target：要更改的数据源(可以是对象或者数组)

                  key：要更改的具体数据

                  value ：重新赋的值


                                    <!DOCTYPE html>
                                    <html>
                                    <head lang="en">
                                        <meta charset="UTF-8">
                                        <title></title>
                                    </head>
                                    <body>
                                    <div id="app2">
                                        <p v-for="item in items" :key="item.id">
                                            {{item.message}}
                                        </p>
                                        <button class="btn" @click="btn2Click()">动态赋值</button><br/><br/>
                                        <button class="btn" @click="btn3Click()">为data新增属性</button>
                                    </div>

                                    <script src="../../dist/vue.min.js"></script>
                                    <script>
                                        var vm2=new Vue({
                                            el:"#app2",
                                            data:{
                                                items:[
                                                    {message:"Test one",id:"1"},
                                                    {message:"Test two",id:"2"},
                                                    {message:"Test three",id:"3"}
                                                ]
                                            },
                                            methods:{
                                                btn2Click:function(){
                                                    //Vue methods中的this 指向的是Vue的实例，这里可以直接在this中找到items
                                                    Vue.set(this.items,0,{message:"Change Test",id:'10'})
                                                },
                                                btn3Click:function(){
                                                    var itemLen=this.items.length;
                                                    Vue.set(this.items,itemLen,{message:"Test add attr",id:itemLen});
                                                }
                                            }
                                        });

                                    </script>
                                    </body>
                                    </html>
















