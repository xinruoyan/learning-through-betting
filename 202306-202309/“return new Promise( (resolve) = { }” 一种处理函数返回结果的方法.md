#### “return new Promise( (resolve) => { }” 一种处理函数返回结果的方法

​    创建函数，通过调用函数，返回运行结果，是我们在编程中使用非常普遍的一张编程方式。在学习使用node.js的过程中，我个人时常有遇到主程序调用返回的结果是“undefined”，反复检查函数也没有问题，单独运行也能打印出运行的结果，但主程序调用就是“未定义”，通过反复观看mixin 机器人视频教程，了解到老师在处理promise回调函数，使用了new Promise( (resolve)的方法，于是也尝试在编程中使用，每次都能比较好解决了函数调用return 结果的问题，一些是其中一个使用案例，仅供大家参考，如果问题可以随时指出，同时也希望如果有好的方法也请告知，互相学习分享。

#### 1.函数通过return 返回 该user_id 下的所有接龙记录，并以数组的方式返回结果。

<img src="https://raw.githubusercontent.com/Dada01Github/images/master/image-20230722230905931.png" alt="image-20230722230905931" style="zoom:67%;" />

#### 2.通过引入return new Promise( (resolve) => { }优化后的函数，可以实现当函数被调用时，结果正常返回。

<img src="https://raw.githubusercontent.com/Dada01Github/images/master/image-20230722225947905.png" alt="image-20230722225947905" style="zoom: 67%;" />

###### 3.附录（修改后的代码）

```
//Function check_jielong_info
async function Check_jielong_Info4user(user_id){
  return new Promise( (resolve) => {
  Jielong.findAll({where:{user_id}}).then(async message =>{  
  contexts ={};
  let days = 0;
  let durations = 0
  
  for(var i=0;i<message.length;i++){
    const date= message[i].memo
    const context = message[i].context
    const duration = message[i].duration
    contexts[date] = context
    days += 1
    durations += duration
  }
  List_Info = [contexts,days,durations]
console.log(List_Info)
resolve(List_Info)
})
})
}
```

