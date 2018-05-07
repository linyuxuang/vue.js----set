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
  
