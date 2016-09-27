#angular

## 1.设置快捷键模板

- file->settings->live template -->javascript-->添加快捷-->define

## 2.创建制定文件后缀

- new edit file template -->"+" 设置文件名字扩展名字即可

## 3.安装mark down 插件

- file-> settings->plugin-->browser responstory  -->mark down navigator

## 4.框架和库

- 一个是提供房子的，另一个是自己搭建房子，只提供方法；

## 5.MVC MVVM

- MVC: model: 数据  view :视图  c :Controler 
- MVVM: model 数据 view viewModel视图模型   model-view-viewModel

## 6.命名空间的缺点：

- 调用过长，不能完全避免名字冲突
-  seajs(cmd)  requirejs(amd) commonjs(node )

## 7.安装angularjs

- npm node package manager   安装完node 之后就会有此功能
```
npm install angular  安装之后就会node_modules 文件夹s
```

## 8.angularjs使用

- 1.引入angular
- 2.设置ng-app
- 3.ng-model="name" 进行双向绑定
- 4.{{name}}

## 9.表达式闪烁

- 是因为angularjs没有加载完
- 通过ng-bind 只能绑定单一的数据避免闪烁，且不能嵌套 (必须加载标签中 而且不能绑定多个)
- 绑定多个 ng-bind-template="{{name}}{{age}}"  不能嵌套 标签内容为空
- ng-cloak 防止闪烁 实现原理就是先隐藏标签（通过样式去隐藏），当angular 完成后再显示自动被移除ng-cloak
- 此时所有数据都绑定在了根作用域下，没有实现模块化

## 10.模块化
- ng-app="module"
    //创建
    //para1 模块名字
    //para2 依赖的模块 没有就是默认[],要是不写就不是创建模块了，就是获取了
    //para3 配置函数
    var app = angular.module('module', []);
    //para1 控制器的名字
    //para2 控制器的函数
    //特点 买一送一$scope

    //不建议在$rootScope在控制器中声明  一般放在run中
    ```
    app.run(["$rootScope",function ($rootScope) {
        //初始化全局变量
        $rootScope.name = 'xxx';
    }]);
    ```

        //参数顺序可以变，但是名字不可以
    ```
    app.controller('c1', ["$scope", "$rootScope", function ($scope, $rootScope) {
        //添加一个属性在当前作用域
        $scope.name = 'lalal';
        //控制器和我们的dom标签是平行的，作用域的范围就是当前标签的管理范围
    }]);
    app.controller('c2', ["$scope", function ($scope) {
        $scope.name = "sss";
    }]);
    //angular 提供了数组的方法防止压缩，原因是字符串是不会被压缩的
    /*app.controller('c2', ['$scope', function ($scope) {
        $scope.name = "sss";
    }]);*/
    ```
    
## 11.函数
  
   //<div ng-controller="c1">
   //    {{age}}
   //    <div ng-click="add()">点击</div>
   // </div>  
    
    
    ```
     var app = angular.module('myModule', []);
     app.controller('c1', ['$scope', function ($scope) {
            $scope.age=1;
            $scope.add=function(){
                $scope.age++;
            }
            $scope.fn = function () {  
               return 100;
               //双向绑定是通过脏值检查来实现的，若数据变了，脏值检查至少要执行2次
            };
        }]);
     ```
## 12.数组 对象
     循环谁就写在谁的身上
             track by $index 添加此句话是为了避免内容有相同的情况发生
             只要有repeat就会创建作用域
             ng-init=就是在当前作用域下声明一个变量存储值
             
         <li ng-repeat="value in arr track by $index">
                 {{value}} {{$index}} {{$even}}
             </li>
              <li ng-repeat="(key,value) in phones track by $index " ng-init="par=$index">
                  {{value.name}}
                  <ul>
                      <li ng-repeat="(key1,value1) in value.type track by $index">
                          {{value1}}{{key}}{{key1}}
                      </li>
                  </ul>
              </li>
             <li ng-repeat="value in phones track by $index " ng-init="par=$index">
                 {{value.name}}
                 <ul>
                     <li ng-repeat="(key1,value1) in value.type track by $index">
                         {{value1}}{{par}}{{key1}}
                     </li>
                 </ul>
             </li>
              
         <ul>
                     <li ng-repeat="(key1, value) in obj">
                         {{key1}} {{value}}
                     </li>
          </ul>
          
## 13.bootstrap  
- 样式框架,提供了样式库，
  ```
   npm install bootstrap
   ```
        