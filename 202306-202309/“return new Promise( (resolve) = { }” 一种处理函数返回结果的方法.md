#### “return new Promise( (resolve) => { }” 一种处理函数返回结果的方法

​    创建函数，通过调用函数，返回运行结果，提高了代码的可重用性，可维护性和可读性，是日常编程中使用非常普遍的编程方式。在学习使用node.js的过程中，本人时常有遇到主程序调用返回的结果是“undefined”现象，单独运行验证代码可以获得预期的结果，但封装函数调用，主程序就是报错“未定义”；多次运行都是同样的结果。通过观看mixin 机器人视频教程，了解到老师在处理promise回调函数时，使用了new Promise( (resolve){}的方法，于是也尝试在编程中使用，能比较好解决了函数调用return 结果的问题，以下是其中一个使用案例，仅供大家参考，如有问题可以随时指出反馈；同时也希望如果有好的方法也请告知，互相学习进步。

#### 1.函数通过return 返回 该user_id 下的所有接龙记录，并以数组的方式返回结果。

<img src="https://raw.githubusercontent.com/Dada01Github/images/master/image-20230722230905931.png" alt="image-20230722230905931" style="zoom:67%;" />

#### 2.通过引入return new Promise( (resolve) => { }优化后的函数，可以实现函数被调用时，结果正常返回。

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

