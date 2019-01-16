# MVC小解

> MVC 本质是一个后期总结出来一个从控制器到视图渲染的一个通用的模式，Model、View、Controller，（视图控制模型）

## 1. SpringMVC(以springMVC为例)
>在springMVC中有一个非常重要的流程，（从浏览器与程序交流的全生命周期）


![](https://raw.githubusercontent.com/MarkXv/staticFile/master/img/MVC/MVC_simple.png)
1. 浏览器发起请求
2. 在前端控制器（DispatcherServlet）调度到处理器调度器中
3. 在处理器调度器中根据URL匹配handler
4. 执行处理器适配器
5. 匹配handler处理器
6. 在handler返回处理结果modelAndView
7. 在处理器适配器，将ModelAndView返回前端控制器中
8. 前端控制器将modelAndView返回到视图解析器中
9. 视图解析器返回view
10. 在视图渲染中的过程中（model填充到view），响应完成

----
__核心前端控制器org.springframework.web.servlet.DispatcherServlet__




## 2. MVC的浅析
> MVC 只是开发中的一个方法论，  
> 将Model，View，Controller进行进行隔离，各个层级之间使用接口调用（有些接口调用是包装好的）  
> Model我们理解为在Controller之下的数据的一个整合打包成一个前端需要的数据集合，  
> View就是对我们拿到的数据进行渲染展示
> Controller就是对各个页面之间的跳转，并且将所需数据携带到各个页面

## 3. 其他
> 在其他地方我们可以把Model层理解为数据的准备层，View就是渲染展示层，Controller就是逻辑跳转层（这个过程携带数据转）  
> 三个层次相互隔离，在开发中可以进行单独测试，  
> 可以单独测试数据层的准备情况，  
> 视图渲染层的可以单独测试，  
> Controller层可以单独测试跳转，  
> 同时也可以进行组合测试