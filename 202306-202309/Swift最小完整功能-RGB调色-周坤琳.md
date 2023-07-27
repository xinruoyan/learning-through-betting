# Swift最小完整功能 | RGB调色

周坤琳	2023/07/27


![img](https://github.com/zhoukunlin/ImageBed/blob/main/配图库/1.PNG?raw=true)



# **隐于市,独木成琳**

为了更好的阅读体验,可以扒拉到文末从「**阅读原文**」进入飞书文档.或者进入文档网址: https://kxv36hgn51.feishu.cn/wiki/S6Ekw27JSic7hNk1kBKc9lyan64?from=from_copylink

> For a better reading experience, you can scroll to the end of the article from the "read the original text" to enter the Flying Book document. Or you can go to the document website. 





# **开篇序言**

> opening preface

![img](https://kxv36hgn51.feishu.cn/space/api/box/stream/download/asynccode/?code=MWRhZTQwNDU5ZGY1MDgzZTc4NjkwZmZkODI3YTI4MzRfNHNYd0l4d0RoSHpvOWQzeFV4WG43VUFEZGRLRFRpalVfVG9rZW46TktZaGJpamtpb3RSUHB4Y0c5dWNPTEZPbnBiXzE2OTA0NjYwNjc6MTY5MDQ2OTY2N19WNA)

**Swift** **是开发****iOS****应用的编程语言**,通常咱们在学习新东西的时候会去看书、看教程、报培训班、加社群、请教老师……并从基础语法学起.但是这回不一样了,苹果公司也是怕你学不会,还专门开发了学习Swift的游戏Playgrounds

> Swift is the development of iOS applications programming language, usually we learn something new when we will go to read books, watch tutorials, enrolment training courses, plus community, ask the teacher ...... and learn from the basic syntax. But this time it's different, Apple is also afraid that you can't learn, but also developed a special game to learn Swift Playgrounds!

![img](https://camo.githubusercontent.com/827311792e01f2135d052156472cbe4426b3de846acf16419a7048539a4dd190/68747470733a2f2f6b7876333668676e35312e6665697368752e636e2f73706163652f6170692f626f782f73747265616d2f646f776e6c6f61642f6173796e63636f64652f3f636f64653d4f5463324d545a685a444e6d5a54566b4f4459784f546b784e6d4e6d4e325668597a466a4e6a5a6d4e7a6c665346417956455a7956586734616d5a6f596d6c58525670305a486c6c4e7a56755a5670464d585a69566a4666564739725a573436566c5636596d4a4a61484a34623246444e3246345254524f536d4e73556b5652626b4a69587a45324f5441304e6a4d314f4459364d5459354d4451324e7a45344e6c39574e41)

想玩的小伙伴可以在Apple store 里下载,要的就是**人人能编程,人人能创造,**这大大降低了学习编程的门槛,**学起来跟玩似的**,学习资源也相当丰富,就看你愿意投入多少时间了.

> Want to play partners can be downloaded in the Apple store, to be able to program everyone, everyone can create, which greatly reduces the threshold for learning programming, learning to play like, learning resources are also quite rich, depending on how much time you are willing to invest.

**不管学什么都需要花时间,并且是很多时间****,**咱们要有个心理准备,**低估投入时间的长度会备受打击****.** “我都学了一年了,怎么还是没学会?”,可事实上一年远远不够,光学一门编程语言也远远不够,甚至还要顺带着学一个像PS那样的**UI****设计软件** —— **Figma ,**这是专门用来设计交互界面的. 所以,路漫漫其修远兮,一步一步的来,只要肯放弃,就会发现……躺平真的是太舒服了……所以如果你下写决心要学,**那么一开始咱们就要做好长期投入的准备**,生死看淡不服就干,**用心平气和的心态每天在代码里“泡一泡”,让它成为身体里的一部分,就像你用手机一样自然,**这个过程中你甚至还会找到乐趣,从而根本停不下来,不让我学就浑身难受!

> Whatever you learn, it takes time, and a lot of time, and we need to be prepared for the shock of underestimating the length of time invested. "I've been learning for a year, why haven't I learnt?". But the truth is that one year is not enough, nor is learning a programming language, nor is learning a UI design software like PS -- Figma, which is specifically designed for designing interactive interfaces. Therefore, the road is long and its cultivation far away, step by step, as long as you are willing to give up, you will find ...... lying flat is really too comfortable ...... So if you write a determination to learn, then at the beginning we have to do a good job of long-term commitment to the preparation of life and death to look at the light do not serve with Peace of mind every day in the code "bubble", let it become a part of the body, as you use the phone as natural, the process you will even find fun, and thus simply can not stop, do not let me learn all over the body!

我刚学完Python编程语言就义无反顾的投入到Swift的怀抱.也做了很多笔记和归纳,如果任其躺在笔记本里就太浪费了,所以我想与你分享,希望能进一步降低学习的门槛,《Swift最小完整功能》系列会不定期更新,**这个系列不会按部就班的罗列Swift的各种基础知识,咱们不做准备工作,直接上手,**在实际开发的过程中就把知识学了,**但这并不意味着容易,需要你跟我一起多敲代码,并做好总结和归纳**.说一千道一万,不如实际跑一遍,实践才是快速入门的阶梯.

> I've just learnt Python and I've jumped into Swift without a second thought. Also made a lot of notes and summaries, if you let it lie in the notebook is too wasteful, so I want to share with you, I hope to further reduce the threshold of learning, "Swift minimum complete functionality" series will be updated from time to time, this series will not be step-by-step listing Swift's various basics, we do not do the preparatory work, directly on the hands of the actual development of the process of the knowledge of the learning, but it does not mean easy, need you with me to knock more code, and do a good job of summarising and summarising. But this does not mean that it is easy, you need to knock on the code with me, and do a good job of summarising and summarising. Said a thousand words, not as good as the actual run once, practice is the ladder of rapid entry.

作为一名平面设计小美工,对颜色是十分敏感的,今天这第一篇就**做个简单的「调色」功能**吧,只需要拨动R、G、B三个滑杆就能改变整个背景的颜色.

> As a small graphic design artists, the colour is very sensitive to this first today to do a simple "colour" function, just toggle the R, G, B three slider will be able to change the colour of the entire background.





# **先看效果**

> Let's see the effect first

![最终效果](https://github.com/zhoukunlin/ImageBed/blob/main/配图库/RGB-app.mp4)





# **安装Xcode**

> Installing an Xcode application

打开Apple Store,搜索: **Xcode** ,点击获取,不出意外的话,这app大小有7个多G……我这已经下载过了,显示的是“打开”,请稍等片刻,跟着安装向导完成安装,

> Open Apple Store, search: Xcode, click to get, not surprisingly, the size of this app has more than 7 G ...... I have downloaded this, the display is "open", please wait a moment, follow the installation wizard to complete the installation, and so on.

![img](https://kxv36hgn51.feishu.cn/space/api/box/stream/download/asynccode/?code=ODIwZWFlY2RmZTU2ODE1NGFiZDM5NjhmMWU3ZTdmZjZfa3dsOE83bEZZNW81RnpHRktFTmJtME5ycUtJUlFGTlhfVG9rZW46R0tRRWJDaUVUb2JpaXF4bEQ4Y2NzVVR6bkNjXzE2OTA0NjM1ODY6MTY5MDQ2NzE4Nl9WNA)![img](https://kxv36hgn51.feishu.cn/space/api/box/stream/download/asynccode/?code=ZGRjYTM5YzE1YzgyOTliMTlkZWM3MWRkMGVkY2ViZWFfVGdZUmVBYmlBUmwxc0RpcWhBQVlvUGFtazVQbHU0eXZfVG9rZW46TUdkVGJoZnFVb29VV3J4TDJ1emN4Rk1KbmVjXzE2OTA0NjM1ODY6MTY5MDQ2NzE4Nl9WNA)

**Xcode集合了多个开发环境**,包括iOS(手机)、iPadOS(平板)、macOS(电脑)、tvOS(电视盒子),甚至到版本15的时候,**还支持开发VisionOS(头显),**在安装的时候你按个人的需要选择,默认安装iOS和macOS,后期也可以单独获取其它OS的开发支持,大小基本都在3G以上.

> Xcode collection of a number of development environments, including iOS (mobile phones), iPadOS (tablet), macOS (computer), tvOS (TV box), and even to version 15 of the time, but also supports the development of VisionOS (headset), in the installation of the time you choose according to the needs of individuals, the default installation of iOS and macOS, and later you can also get the support of the development of other OS, the size of the basic are more than 3G.

![img](https://kxv36hgn51.feishu.cn/space/api/box/stream/download/asynccode/?code=MTc3NjM0Nzc0ZTY0ZmM4YWNkMGI2ZGM0YjM3YmY2ZDVfRk9FOVpiSGFmUThRZHBZVDN3WXdqOVE4d3VZNWV5bXNfVG9rZW46VHgyZGJvV3VRbzdIWVd4TXZmZ2NXVGk2bkFnXzE2OTA0NjM1ODY6MTY5MDQ2NzE4Nl9WNA)

不出意外的话安装完是这个样子:

> Unsurprisingly the installation looks like this.

![img](https://kxv36hgn51.feishu.cn/space/api/box/stream/download/asynccode/?code=YTYwNjBlY2RjNWE4MWIwNGU5NDIwODRlYmVkYWEyZWVfd05mMzhDWjZ5RkJaam9heEJaTjdNUnc1Q2xHZlJNdnNfVG9rZW46QzJVQmJxV2Iybzh1eVd4UU41NGNOczhVbjVjXzE2OTA0NjM1ODY6MTY5MDQ2NzE4Nl9WNA)

我Xcode的版本是**14.3.1**, 正常情况下,你看到的右边灰色区域是有一个示例或者空白,咱们要开发的app工程软件就罗列在这里了.不同版本会有细微差异,稍微有一点不同,对于咱们小白来说就是天大的坎,所以减少卡壳的概率,建议与这个版本一致或者差不多,减少不必要的时间浪费,待学会之后,用其它版本的就没那么大的隔阂了.

> I Xcode version is 14.3.1, under normal circumstances, you see the right grey area is a sample or blank, we want to develop the app project software listed here. Different versions will have slight differences, a little different, for us white is a big hurdle, so to reduce the probability of jamming, it is recommended that this version of the same or about the same, to reduce the unnecessary waste of time, to be learnt after the use of other versions of the gap is not so big.

一切就绪,开干!

> It's all set. Let's go!

# **直接上手**

> Get right to it.

新建一个工程文件:

> Create a new project file.

![img](https://kxv36hgn51.feishu.cn/space/api/box/stream/download/asynccode/?code=Yjg4ZDYyMjU1ZGNlMjc2ZDc0NjFjOWIzZmFmZDIzM2Vfd2FOalpUb3JSSkRhOFRXUWdib2dNQkdMQmVFYmxiOVZfVG9rZW46UHpMSmJXVW9tb3ViVjV4QjAxeWN3b1RmbnViXzE2OTA0NjM1ODY6MTY5MDQ2NzE4Nl9WNA)

取个名字,点击下一步:

> Give me a name, click next.

![img](https://kxv36hgn51.feishu.cn/space/api/box/stream/download/asynccode/?code=YTUxNzIxZWNjY2I1MTViYTQ5NGVkODhkYzJjNWJhMmZfZmF1aEhYSE5BUGN1TFlrZlV1QVNRTkQ5OHlMMjY5bGVfVG9rZW46RnhXV2JzRmNKb1RjVld4ODFEOGNjR1YybmZmXzE2OTA0NjM1ODY6MTY5MDQ2NzE4Nl9WNA)

按个人喜好指定项目的目录所在地,也方便以后你能找得到:

> Specify the location of the project's directory according to your personal preferences, so that you can find it later.

![img](https://kxv36hgn51.feishu.cn/space/api/box/stream/download/asynccode/?code=ZmU4MzJlYmMwYmQ2ZTViNGYwNzdmM2E2NjZjZWFlZWFfcDVwTnVqdHowc0NReWZjUVNjQktMY0J1eGNSeVdDVFFfVG9rZW46Q3pCOGI1U0pSb0ZQVW94WVlKM2NaS0wwbjFlXzE2OTA0NjM1ODY6MTY5MDQ2NzE4Nl9WNA)

**先整体看看有些什么功能**,似乎没那么难以理解:

> Let's take a look at the features as a whole. They don't seem to be that difficult to understand.

![img](https://kxv36hgn51.feishu.cn/space/api/box/stream/download/asynccode/?code=ZWViMWI2OGQyMzEwNWNlNWFjNTZiNjY5ODI2YWNiMWNfZkJHTDVMTHlwd2F6a3paZGc2SjR0ak1OcVV0dDBCNEVfVG9rZW46VFVxemJCakhzb0pQQ2R4dFFpdWNWaDRNbmpnXzE2OTA0NjM1ODY6MTY5MDQ2NzE4Nl9WNA)

工程文档建好了,在**`ContenView.swift`**文档里,映入眼帘的是这串代码,里面包含了图标和文字的内容:

> Now that the project file is built, in the ContenView.swift file, you'll find this string of code, which contains the contents of the icon and the text.

![img](https://kxv36hgn51.feishu.cn/space/api/box/stream/download/asynccode/?code=Y2U5YmUzMjU3N2MxYmRmZWE4MGFmYjI1OTY3NjhkNzBfa3k2Q2NrRDZ0RTJtR09nQ1IxMEFDbjh5czVBQkZGQ0NfVG9rZW46VU1jYWJkQkZVb2pyc0d4M05JTWNITndLbkZjXzE2OTA0NjM1ODY6MTY5MDQ2NzE4Nl9WNA)

![img](https://kxv36hgn51.feishu.cn/space/api/box/stream/download/asynccode/?code=MzIzNjMwOTJlYjhjNTUyOTZlMTU5YTMxOWU5M2U5NGZfcVhhUnh5cUZVdk9na2xYemZJQXVUcElRamxRVXltZk5fVG9rZW46UHdQZWJka1Vxb0QzNnR4bmF5T2NYOVIwbnloXzE2OTA0NjM1ODY6MTY5MDQ2NzE4Nl9WNA)

看起来也没那么难嘛,先不管每一个单词是什么意思,整体的框架就是这样,先有个大致了解,接下来咱们就改动一下代码,选中**`VStack{}`**里图标、文字的代码,按快捷键: **`⌘ + /`**,把它们全部注释掉或者直接删除,意思就是告诉电脑,这几行代码不用管它,不要运行.然后右边的手机界面就一片空白了,等待着你的创作:

> It does not seem so difficult, regardless of what each word means, the overall framework is this, first have a general understanding of the next let's change the code, select VStack {} in the icon, the text of the code, press the shortcut key: ⌘ + /, they are all commented out or deleted, which means that you tell the computer, these lines of code do not care about it, do not run. Then the right hand side of your phone will be blank, waiting for you to create something: ⌘ + /.

![img](https://kxv36hgn51.feishu.cn/space/api/box/stream/download/asynccode/?code=YmViMmY1ZDg2NTI4YjY5NDNhYmVmZmU5YzMwOTkxOWRfWmFvdmJzQ09vaVgyWXFoOEZSUjBBSjhwY0VvNEFGeWhfVG9rZW46WE1JVmJRenE1b1FqYmN4T2trWmNEc0lvbldnXzE2OTA0NjM1ODY6MTY5MDQ2NzE4Nl9WNA)

这个**`VStack{}`**就像一个隐形的表格,让里面的元素以竖向排列的方式显示,所以咱们把RGB的字样显示出来,文字需要用**`Text("")`**表示,双引号里写上要显示的文字,表明这是字符串:

> This VStack{} is like an invisible table, so that the elements inside are displayed vertically, so let's display the RGB text, the text needs to be expressed in Text(""), and the text to be displayed is written in double quotes, indicating that this is a string.

![img](https://kxv36hgn51.feishu.cn/space/api/box/stream/download/asynccode/?code=NjIyMGFhNjNmN2UyZGM1NmY5MjE1MjJmYjk4YWNjZTFfeVBRM1VzNVNwQzRGUXhBTmhTYUJ0QnZZT0VXRGd1Z2pfVG9rZW46VlJyY2JxTG13bzVWd0x4dk4zNGNqWTA3blZkXzE2OTA0NjM1ODY6MTY5MDQ2NzE4Nl9WNA)

**`VStack{}`**是竖向排列,那是不是就有横向排列?

> VStack{} is vertically aligned, does that make it horizontally aligned?

嗯,很聪明,横向排列用**`HStack{}`**,把这三行字符串横着排看看效果:

> Well, that's clever, horizontally using HStack{}, put the three strings horizontally and see how it works.

![img](https://kxv36hgn51.feishu.cn/space/api/box/stream/download/asynccode/?code=YzU0MTVjM2UwODU2MDNjMGM0OWI5MmU0MzNjYWQ0M2FfMWJFcnhvN1lZQk1BOEdnQ2pYSWNzV1N6MUdWempIMWJfVG9rZW46VVk2UWJkVURFb2N5SWt4S2lVVmNNbFNYbjZnXzE2OTA0NjM1ODY6MTY5MDQ2NzE4Nl9WNA)

接下来加入**`Slider()`**, 没错,字如其用,就是一个滑杆,编程就一句话的事儿.那么这个滑杆是怎样的呢?在小括号里描述它的“长相”:

> Next, add Slider(), which is exactly what it says, a slider, and programming is just a matter of words. So what does this slider look like? Describe what it looks like in parentheses.

```Swift
Slider(value: Binding.constant(1))
```

![img](https://kxv36hgn51.feishu.cn/space/api/box/stream/download/asynccode/?code=NzQ5ZmUzYzk5ZjcxMjExMWU4YTE1MTE2NGQ0MjliZTZfSVZQaWFwYTE0T3dYc3R6Uzg0Z1F3RzMyZFF4cUJxakhfVG9rZW46TUd0VmJtd0RPb1czWUd4VFlOaWMzS2xabjZkXzE2OTA0NjM1ODY6MTY5MDQ2NzE4Nl9WNA)

意思是说,这个滑杆有个值(**value**),给它指定一个样式(**Binding**),让它保持默认即可**constant(1)**

> Meaning, this slider has a value, assign it a style (Binding), let it keep the default constant(1)

定义好一个就复制粘贴,一共要有3个滑杆,**注意要与HStack{}模块对齐**;因为它们是**同属于****`VStack{}`****里的模块**,如果代码的区域太小了,可以把最右边的窗口先收起来:

> Define one and copy and paste it. There should be 3 sliders in total. Be careful to align them with the HStack{} module; since they belong to the same module in the VStack{}, if the area of the code is too small, you can put the rightmost window away first.

![img](https://kxv36hgn51.feishu.cn/space/api/box/stream/download/asynccode/?code=MTI2NGI2OWVkYTIwMTRmNGEyYTk1ZjZlZTk3Nzg5ZjBfZ1dNaUZ0MkkwM0VVQWxkbmZ5RlVPbjJ4Vll2aU53VG9fVG9rZW46UkR5MGJlRU9yb2RjcXp4RnBTaWNOQmxnblJiXzE2OTA0NjM1ODY6MTY5MDQ2NzE4Nl9WNA)

这下子代码层次就明显了,世事无常,大肠包……两个小肠……

> Now the code hierarchy is obvious, the world is unpredictable, the large intestine package ...... two small intestines ......

![img](https://kxv36hgn51.feishu.cn/space/api/box/stream/download/asynccode/?code=MjBjYWMxZTUxNzJjNmUwOTcwMDM0ZGI5OTNkNDY5N2FfUE95MzlRNE54UEtNS1JHUFpSSXZSZlJIVE5xSU9KTTNfVG9rZW46RlQySGIyMGRIb08xaHF4ZGdJd2NYRnU1bkhnXzE2OTA0NjM1ODY6MTY5MDQ2NzE4Nl9WNA)

文字和滑杆都粘在一起,好嘛,连它们都在秀恩爱! 不能忍! 得把它俩分开! 在这两个模块之间输入**`Spacer()`**

> The text and the slider are stuck together, well, even they're in love! I can't stand it! We have to separate them! Type Spacer() between the two modules.

![img](https://kxv36hgn51.feishu.cn/space/api/box/stream/download/asynccode/?code=ODgwOTk0NTE3NzI1NGYwNWRjMTBjZGE4YTg5YzBlODRfc0ZKdG1JZG5la0FiQnppYW9uT1N5U3JBSG12V25JQWRfVG9rZW46Rnh5R2JucjVPb0FFbGt4bGc1QmNKTmJYbnllXzE2OTA0NjM1ODY6MTY5MDQ2NzE4Nl9WNA)

爱情令人盲目,我居然这么狠心……

> Love is blind, I can't believe I'm so cruel ......

作为平面设计的我强迫症发作了,眼看着这滑杆两端都顶到头,实在影响美观,所以让两端稍微留点空间:

> As a graphic designer, my OCD kicked in and I saw that both ends of the slider were pushing up against my head, which was aesthetically displeasing, so I left the ends a little bit of space.

![img](https://kxv36hgn51.feishu.cn/space/api/box/stream/download/asynccode/?code=ZmI1ZjRjZTE5OGI2YzQ1NzQ4ZDQ5OGYwMDBlYjJmNjNfMzFuQXpQdGpRTkQwSFVWQ1NETEdncDhZQmp4NGExaHFfVG9rZW46STFzV2JCeWU1b0xkalF4NExzdGNFSGMwbnRiXzE2OTA0NjM1ODY6MTY5MDQ2NzE4Nl9WNA)

那就对整个**VStack{}模块加个属性**,方法也很简单,就在后面输入小数点,然后指定样式:

> Then add an attribute to the entire VStack{} module, which is as simple as typing a decimal point after it and specifying the style.

```Swift
VStack{
    ……
    }.frame(width: UIScreen.main.bounds.size.width * 0.7)
```

啥意思呢?

> What does that mean?

给这个**`VStack{}`****模块**指定一个样式(**`frame`**),整体的宽度(**`width`**:)是个**`UIScreen`**,其中主屏(**`main`**)的边界(**`bounds`**)尺寸(**`size`**),它的宽度(**`width`**) * 0.7 ,也就是说占整个界面的70%,这写文章的方式进行编程也是没谁了,英文也顺道学起来了,最后来看看效果:

> to this VStack {} module to specify a style (frame), the overall width (width:) is a UIScreen, which is the main screen (main) of the border (bounds) size (size), its width (width) * 0.7, that is, accounting for 70% of the entire interface, which writes an article on the way to program. There is also no one, in English! also learnt along the way, finally to see the effect: the

![img](https://kxv36hgn51.feishu.cn/space/api/box/stream/download/asynccode/?code=YzJhZjY3MTJhMzIxZjliMzNiMDljOWZiMWY4YTNkM2VfNFljUk1maURleXczTlVEaWR6WjF2TFVaRlNQQ256WGxfVG9rZW46UktIT2JaWjU4b1dKSmp4VXN0NWNWNWxHbmVlXzE2OTA0NjM1ODY6MTY5MDQ2NzE4Nl9WNA)

这时站在背后的老板没好气的说:“文字太小了,你们这些臭搞设计的能不能把文字弄大一点?”.

> At this time the boss stood behind the back of the boss said in a bad mood: "The text is too small, you stinking designers can not make the text a little bigger?" .

那简单,也就是一句话的事儿嘛,**给文字Text("")加几个属性**.

> That's easy, it's just a matter of adding a few attributes to the text Text("").

```Swift
.font(.title)   // 文字放大
.fontWeight(.light)     // 字重(字体细一点)
```

![img](https://kxv36hgn51.feishu.cn/space/api/box/stream/download/asynccode/?code=ODk1MzEwZDAxM2RlMzhhMmE3MTMxMTdjNmMxZTBiNDBfQ1hHSVFYUGQ0VUhKRUF1Q29MQXFROGoxNVBJNVl5dk1fVG9rZW46TFRNYWI4aFg3b3ZkM1d4UlBKbmM5RFp6blZBXzE2OTA0NjM1ODY6MTY5MDQ2NzE4Nl9WNA)

原来这么简单,感觉只要懂点英文就会编程了.然后也是简单的复制粘贴,让这3个文字都用一样的款式……

> It's so simple. I feel like if you know a bit of English, you'll be able to program it. Then it is also a simple copy and paste, so that the 3 texts are the same style ......

唉……刚还夸你聪明呢,一个一个的去指定款式重复的代码就太多了,这还只是3个,要是有1000个,你难道也要一个一个的指定吗?**能让机器去做的,就千万别让人来干**.既然文字**`Text("")`****是包含在整个****`HStack{}`****模块里的**,只需要对它指定款式不就好了?

> Alas ...... just also praised you smart it, one by one to specify the style of duplicate code is too much, this is only 3, if there are 1,000, you do not want to specify one by one? can let the machine do it, do not let people do it. Since the text Text("") is included in the whole HStack{} module, just specify the style for it, right?

![img](https://kxv36hgn51.feishu.cn/space/api/box/stream/download/asynccode/?code=NTM1MTI2OWE1NGQwMzliODdkOTQyMmFmMjZiOWI1NTdfaThGaVRVVmRnNkxYaHdvYkxTQ3RQeHlpMGt5WHJRd2ZfVG9rZW46S1QyaWJybDZBb25OOHh4WnVZb2NRNHYxbnpnXzE2OTA0NjM1ODY6MTY5MDQ2NzE4Nl9WNA)

可是这该死的强迫症,这3段文字都粘在一起,我是单身狗见不得秀恩爱,咱活学活用,同样也是用**`Spacer()`**把它们分开, **呵! 我真是个人才……**

> But this damn OCD, these 3 paragraphs of text are stuck together, I am a single dog can not see the show of love, we live and learn, also with Spacer () to separate them, heh! I'm really talented ......

![img](https://kxv36hgn51.feishu.cn/space/api/box/stream/download/asynccode/?code=ZmM0ZTVhNmI1OGEzNjM0Mjk4ODUzZjBlMzJlMWY5ZmJfWDdIQUZJMjl5SWxSajdnR3JUaGd4UElzMXdFTU1XVkVfVG9rZW46SnJEVWJqakVXb3Y0OUd4S3R4U2NOU1lVbjZRXzE2OTA0NjM1ODY6MTY5MDQ2NzE4Nl9WNA)

最后为了这3个横排的字符串不被动态岛所影响,需要**预留一些空间**给它,**就像做事一样,留有一丝回旋的余地:**

> Finally, in order for the three horizontal strings not to be affected by the dynamic island, it is necessary to leave some space for it, as in the case of doing things with a margin of manoeuvre.

```Swift
VStack{
    ……
    }.offset(x: 0, y: 50)    // 离动态岛远一点
```

![img](https://kxv36hgn51.feishu.cn/space/api/box/stream/download/asynccode/?code=YWQxOTc0ZmU4YTk1ZGIwYzA0ZmI5YzFjMGQ1ZDYyZWFfOTFmYXV4NHlCa1FNazhjcnVkS3FHd09jQVZXRllXYTlfVG9rZW46T2JPQWIzN29Lb2NhTm94T3JWY2NLV05RbnBiXzE2OTA0NjM1ODY6MTY5MDQ2NzE4Nl9WNA)

![img](https://kxv36hgn51.feishu.cn/space/api/box/stream/download/asynccode/?code=ODU1YWU1MzczMTA4YzczMTIwNzhmMzc4MmY2NDMzNzRfbnZVTUdLVENJNzNQb1c0VHAzOWhURHUzMFgwbHdQMGJfVG9rZW46WE56RmJTUkNBb3dnU2N4V25LcmNWU2k2bjg0XzE2OTA0NjM1ODY6MTY5MDQ2NzE4Nl9WNA)

所以,编程有这么难吗?就跟平时的说话一样. 不过目前咱们操作这些滑杆并不能对背景色有所影响,字符串里的数字也不会变动,为了能让它们关联起来,需要定义3个可变动的变量,关键字是 **`var`**

> So, is programming that hard? It's just like talking. But for now, manipulating the sliders won't affect the background colour, and the numbers in the string won't change, so in order to make them relevant, we need to define three variables that can be changed, the keyword being var.

噢!是不是还有不可变的变量? 对,关键字是 **`let`**不过现在用不着.

> Oh! Isn't there an immutable variable? Yes, the keyword is let, but we don't need it now.

```Swift
var redValue:Double
var greenValue:Double
var blueValue:Double
```

![img](https://kxv36hgn51.feishu.cn/space/api/box/stream/download/asynccode/?code=ZTg5ZDdiNDA4YmI4MjZmZTk4MDZmMjhhZGE4YjFmYTZfQWp4R1BUazd0ZHRUQVRERlpWNUxpd2ttRld2RzlKOVJfVG9rZW46THN3YWJPQm81bzYzajJ4NDVma2NwZnlzbmpmXzE2OTA0NjM1ODY6MTY5MDQ2NzE4Nl9WNA)

从字面上来看就是**红(R)、绿(G)、蓝(B)**三原色的值,对吧,可冒号后面跟着的**`Double`**是个啥?

> Literally red (R), green (G), blue (B) the value of the three primary colours, right, but the colon followed by Double is a what?

唉!**英文不好就是这么恼火啊**,同样是字面上的意思 —— **双倍**,意思是说,**这个****RGB****的值是可以带小数点的**.不过贴心的Xcode会高亮告诉我们一个错误:

> Oh, my God! It's so annoying when you don't speak English well, and it's literally the same thing - double, meaning that the RGB value is allowed to have a decimal point. But the nice Xcode will highlight an error.

![img](https://kxv36hgn51.feishu.cn/space/api/box/stream/download/asynccode/?code=NzM5Y2FlYWNhMmQzMzcwOWIyZjcxYTliYWY2OWFjODBfM3loQzZZVHpGRGg4dXJvT3YxNHZvVkVIVnc0TmxTdmNfVG9rZW46Wm1ydmJiRVVPb1ZHNFN4QmRCdGNIRXdabkc0XzE2OTA0NjM1ODY6MTY5MDQ2NzE4Nl9WNA)

这所谓**牵一发而动全身**,咱们一直修改的这个代码文档**`ContentView.swift`**就相当于宿舍楼一幢,光是咱们在宿舍里敲定了暗号,但不告诉“门卫保安”,人家对不上暗号就不让你过呀!所以还得写个小抄给它:

> This so-called pull one hair affects the whole body, we have been modifying the code document ContentView.swift is equivalent to a dormitory building, the light is that we have finalised the code in the dormitory, but do not tell the guards security, they can not match the code will not allow you to pass ah! So we need to write a cheat sheet for it.

![img](https://kxv36hgn51.feishu.cn/space/api/box/stream/download/asynccode/?code=MTY4MzQ5NzVmZTRlOTMxYzM0YzZhMmVlZDgxNzM4MTRfOUwzSnlZb1BMZ3FNN2NXMm8zMUp3clVWNnY5NkZ5ZjJfVG9rZW46SzhrRmJpUm1Pb1ZRdHF4WXMwUmNwOTFHbm9kXzE2OTA0NjM1ODY6MTY5MDQ2NzE4Nl9WNA)

当然别忘记还有“二幢的保安”**`RGB_appApp.swift`**也抄一份:

> And of course, don't forget to copy the "security guard of the second building" RGB_appApp.swift.

![img](https://kxv36hgn51.feishu.cn/space/api/box/stream/download/asynccode/?code=ZjUxMjdmNDhmMmMzZDE0MmU4MzU1N2ExNWQ3NjEzYmJfMnZvc0hWQ0xiUUVvRmdvNWpXVkMweE1zWUR2WnVXZk5fVG9rZW46STlQd2JZbzdyb0x2STN4SkZYbmNROWdNbmdoXzE2OTA0NjM1ODY6MTY5MDQ2NzE4Nl9WNA)

**这下就串通一气了**,为了能让RGB的数值能随着波动滑杆而改变,就把这字义好的变量**`在双引号里`**用**` \() `**的方式放在字符串里,在Python里叫作“格式化输出**`f-string`**”,只不过是放在大括号里,表明一段文字里这个部分是能随情况变化的:

> Now we're in cahoots. In order to make the RGB value change as the slider fluctuates, we put the literal variable in double quotes in a string using \(), which is called a "formatted output f-string" in Python, but it's in curly brackets to show that this part of the text can be varied according to the situation.

![img](https://kxv36hgn51.feishu.cn/space/api/box/stream/download/asynccode/?code=MzRkZDcxNTVkNjM4YjRkZWY0YTE3Y2EyOTFhYmI3OGRfblFodGlwVnlmRmdyQmV1V3g5S2FYRXZMV0sxM2luSWdfVG9rZW46V2h1ZmI4T2Rkb2RmMEd4RnhaTWNGSVphbjJkXzE2OTA0NjM1ODY6MTY5MDQ2NzE4Nl9WNA)

![img](https://kxv36hgn51.feishu.cn/space/api/box/stream/download/asynccode/?code=NWJhODU4MDMxNjJiMTMwN2Y1MDlmOTU0ZDA4Y2ZjYmNfZVhhenk2Y1NmcjBKWUxyNWVxakhPbjZETkFsZnRMc1VfVG9rZW46T0tuRGI2d0FFb01SY3F4eEl0dmNVc3FpbnhmXzE2OTA0NjM1ODY6MTY5MDQ2NzE4Nl9WNA)

可是这一长串的小数点用不着啊,那就转换成整数:

> But you don't need this long list of decimal points, so convert it to integers.

![img](https://kxv36hgn51.feishu.cn/space/api/box/stream/download/asynccode/?code=M2FjZmU0NTA5MzExYzcwNzQzNTQyM2ZkNWY3MWJjYWFfNmc5ckEzOFM1R3lBTDEwNEZCcXVkbjNySVBITDJyZzFfVG9rZW46RW12U2I5ZndCb1dUcHZ4anVqbWN0QnQ5bjJiXzE2OTA0NjM1ODY6MTY5MDQ2NzE4Nl9WNA)

按照国际惯例,RGB的每一个值都不会超过255,得限制一下:

> According to international practice, each value of RGB will not exceed 255, so there is a limit.

![img](https://kxv36hgn51.feishu.cn/space/api/box/stream/download/asynccode/?code=ODYwODU5NzQxNjUwNjMyYWRmNjA5N2YxZjBiYjg5ODFfbjIzeXJnaEttYjVTa2JpTzhaM1BxdVdMZFVJM0ZMWVNfVG9rZW46TktxRWJWV2Zlb09CZ0t4QXVMWGNoSXNkbldoXzE2OTA0NjM1ODY6MTY5MDQ2NzE4Nl9WNA)

非常好,现在就要实现在拨动滑杆时,能让数值跟着变了,于是用**`@State`**进行一个关联:

> Very good, now we need to implement a way to make the value change when we toggle the slider, so we use @State to make an association.

![img](https://kxv36hgn51.feishu.cn/space/api/box/stream/download/asynccode/?code=YTFkYTI0MjJjN2NmNGE1NjBiYzUwNjBjODRiYThhMDJfV1VXOXJueVZ0MlV2WTZydlBoUXZLb0VnZmJnaXBzWkJfVG9rZW46SnNxUGJsd3hOb2RTQVJ4dmtDc2NrVVNsbmNlXzE2OTA0NjM1ODY6MTY5MDQ2NzE4Nl9WNA)

在滑杆的**value**后面用 **`$`** + **`变量名`**关联:

> Associate the value of the slider with $ + variable name followed by.

![img](https://kxv36hgn51.feishu.cn/space/api/box/stream/download/asynccode/?code=YmEyNjdhNzEzMGMzMDE1OGE4YzdkMDAxYmJhYzk1YzlfeXI4WkY0UlJrWFNiUFRpdUlVVFVyMWhjUHRCVHR0blZfVG9rZW46TlMxdWJJN0JGb2lpMWt4cjgzcWNLSkRzbjFnXzE2OTA0NjM1ODY6MTY5MDQ2NzE4Nl9WNA)

这样就产生了关系,仔细打量目前写的这些代码,所有东西都在整个VStack{}里面,

> This creates a relationship, and if you look closely at the code you've written so far, everything is in the whole VStack{}, and it's all in there.

![img](https://kxv36hgn51.feishu.cn/space/api/box/stream/download/asynccode/?code=ZWJkNzRkZmYyYTQ5MDJhNTdhNzllYTEzNDA2OTE1MDRfbzJndXQwTXhpa3FESXZRckIzaGU1Z2VOOFlPOHpjUkRfVG9rZW46T2dUMmJ6VmdXb0QzSkR4NWkzb2NJMnRRbmdnXzE2OTA0NjM1ODY6MTY5MDQ2NzE4Nl9WNA)

咱们可以把它形象的**看成1楼**,**那么背景就是-1楼了是不?**经过前面所实践的可以知道,**`VStack{}`****是把元素竖着排,****`HStack{}`****是把元素横着排,那么空间上的前后的摆放就要用到****`ZStack{}`****了**,没错,就是靠着这些简单的单词,可以安排元素在“三维空间”里进行摆放.

![img](https://kxv36hgn51.feishu.cn/space/api/box/stream/download/asynccode/?code=YWU2NWQ0ZGZjN2QyYzJkOGMwY2I5ZGEwYzNhYTU1NmZfd2VDTGlZV1JtbUlJVHk2R3RXRVVTQ2JvejNRc2NRVXRfVG9rZW46U2xldGJEdWpCb0Nmd2N4eTNOTGM4MUQxblNmXzE2OTA0NjM1ODY6MTY5MDQ2NzE4Nl9WNA)

![img](https://kxv36hgn51.feishu.cn/space/api/box/stream/download/asynccode/?code=NjE1NTk1NzhjM2RmODE1ZDZlZDBhMTUyNTRjYmU3MTBfN3NNb2VCTjdVNDhvWHJoMXg1bUYxQXN0c3BJcU40bURfVG9rZW46UzR1MmJSV3hub25Sb0J4Mnhvc2NhZEZXbmlkXzE2OTA0NjM1ODY6MTY5MDQ2NzE4Nl9WNA)

在-1楼里加个颜色:

> Add a colour to the -1st floor :)

![img](https://kxv36hgn51.feishu.cn/space/api/box/stream/download/asynccode/?code=YzQyNzk5OTE1MjlmYzNlZDg4ODUxZGNjOTY5ZmQ3ZDhfcm1RMDIwN1NTbjEwSGI2NzdKMnBxY2Jkb1Q4ZEMyT1BfVG9rZW46REtCMmIyb2Nxb1FmUUd4UlNyT2M2bjFmbnpnXzE2OTA0NjM1ODY6MTY5MDQ2NzE4Nl9WNA)

其中红色、绿色、蓝色 均是咱们定义好的变量,是随着滑杆的改变而改变的,所以把变量分别填进去:

> Red, green, and blue are all defined variables that change as the slider changes, so fill in the variables.

![img](https://kxv36hgn51.feishu.cn/space/api/box/stream/download/asynccode/?code=NWNiYmJkODU5NmM1NjVhN2IzMDM0OTNlNzkxMTQ3NmRfZmlwV2taU09oY1RWc000NUZySE9kbXgwUzJaRExsZGVfVG9rZW46Rzl4UWJoU0Z1b01PckJ4Wm5JU2Nkc0hWblV0XzE2OTA0NjM1ODY6MTY5MDQ2NzE4Nl9WNA)

![img](https://kxv36hgn51.feishu.cn/space/api/box/stream/download/asynccode/?code=MzkzZDI3YzA4ZWUyZmIyYTcxODdlYmQ1YjJiZDM1ZWRfdjdMWnNucVZNVlhobXFtQ2pHcWVTWFVQbjZYTDB0MHRfVG9rZW46QjJaMWJkUkc2b0oxS2h4RVhYWWN6a0o2bjZiXzE2OTA0NjM1ODY6MTY5MDQ2NzE4Nl9WNA)

可是,1楼的那些滑杆呢?说好的空间层级呢?咱们颜色代码确实是写在-1楼里,可从效果来看好像-1楼跑到1楼上面去了,**难道要倒过来?**

> But what about those sliders on the first floor? What about the spatial hierarchy? Our colour code is indeed written on the -1 floor, but from the effect of the -1 floor seems to run on the 1 floor above, should we reverse?

![img](https://kxv36hgn51.feishu.cn/space/api/box/stream/download/asynccode/?code=OWQ3ODc0MmVhN2FhOThhMTgyMGYxNzQzMGFmNTMyNThfRVJRUXA2YU92V0E3a1VpT3E5NkdZSHVxMlNYVTJtMk9fVG9rZW46TTR1bGJxT0lCb3FjbVp4RElZaWN2Y2VobkJiXzE2OTA0NjM1ODY6MTY5MDQ2NzE4Nl9WNA)

滑杆出现了,原来这个空间是倒序的,拨动滑杆看看?

> The slider appears, so the space is in reverse order. Toggle the slider and see?

![img](https://kxv36hgn51.feishu.cn/space/api/box/stream/download/asynccode/?code=YzE4MDQwYjJkOWNlZDZkM2M4OWMzMjhiNmY4ZmIxOWNfREN1TXh3SmMxVGtSaVpSdXVmWnlhSk81N0dmRUdYTGRfVG9rZW46UGM0NmJKWmc1b1BjRVZ4c3IzSWNjbVZVbjNjXzE2OTA0NjM1ODY6MTY5MDQ2NzE4Nl9WNA)

可见这背景并不是铺满整个屏幕的,那就加个样式呗,**`.edgesIgnoringSafeArea(.all)`**

> The background is not spread all over the screen, so add a style, .edgesIgnoringSafeArea(.all).

![img](https://kxv36hgn51.feishu.cn/space/api/box/stream/download/asynccode/?code=Nzc0Mzc0YWIzOGUxOGIyYTRmNDY0MDMxZGNlODI1MDFfYTMyT2lqNENtUHloVzNiOGFjcjNtN0J6ZjhpT0hMYmNfVG9rZW46RDU4cWIxOXFVb1RaMHZ4QURzYmN1UDBubnpoXzE2OTA0NjM1ODY6MTY5MDQ2NzE4Nl9WNA)

成功把边缘铺满整个屏幕.**最后还是要在“真机”里测试一下,**按下快捷键 **`⌘ + R`****,**第一次运行测试会稍微慢一点,因为要安装一个虚拟的iPhone,以后就快很多:

> Successfully spreads the edges all over the screen. To test it on the "real" iPhone, press the shortcut ⌘ + R. The first run will be a little slower because you have to install a virtual iPhone, but later on it will be much faster.

![img](https://kxv36hgn51.feishu.cn/space/api/box/stream/download/asynccode/?code=ZDM4NjhjYWEyZGNmNjJjNDI3NTE1NjA5OGFjOWYyOWVfUm96bmpwYU9SUVhaWUl4QXJJSXB6Q29sd2VyV01Db3NfVG9rZW46TzZreWJhSEJEb3Yxbm94RzhpTmNEN0EwblVmXzE2OTA0NjM1ODY6MTY5MDQ2NzE4Nl9WNA)

运行正常,恭喜你,完成了第一个最小完整功能,如果多来几个,是否就可以轻松把Swift学会了?想想就激动!

> Running normally, congratulations, completed the first smallest complete function, if a few more, whether it will be easy to learn Swift? Just think about it!

# **总结归纳**

> summarise

| No.  | **知识点**                                                | 说人话                                  | 举个栗子🌰                                                    |
| :--: | --------------------------------------------------------- | --------------------------------------- | ------------------------------------------------------------ |
|  1   | **VStack{}**                                              | 将元素**竖向**排列;                     | `VStack {    Text("R: 255")    Text("G: 255")    Text("B: 255")}``HStack {    Text("R: 255")    Text("G: 255")    Text("B: 255")}` |
|  2   | **HStack{}**                                              | 将元素**横向**排列;                     |                                                              |
|  3   | **ZStack{}**                                              | 将元素**前后**排列;                     |                                                              |
|  4   | **Text("")**                                              | 显示文字内容,字符串;                    |                                                              |
|  5   | **Slider****()**                                          | 默认滑杆;                               | `Slider(value: Binding.constant(1))`                         |
|  6   | **Spacer()**                                              | 分手用,隔开元素;                        |                                                              |
|  7   | **.frame(width: UIScreen.main.bounds.size.width \* 0.7)** | 设置这个模块占整个界面的比率,也就是70%; | ![img](https://kxv36hgn51.feishu.cn/space/api/box/stream/download/asynccode/?code=ZGNkNzdjMGM1MDMxYjAxZDYxYzg4N2QzNmJlODNjYTdfejEwaHRrUVVHS0ZQVTVLSlNWZERaUTdzVmd0VFJBYzFfVG9rZW46UkxpeWJjQmU5b3Rla3V4d0tObmM4bHl3bjZjXzE2OTA0NjM1ODY6MTY5MDQ2NzE4Nl9WNA) |
|  8   | **.font(.title)**                                         | **文字**要**放大**                      | ![img](https://kxv36hgn51.feishu.cn/space/api/box/stream/download/asynccode/?code=OTkyOWJkMWZjZGIyZTgwMTIzNjBiM2FlNDJhMDYyYmRfbGJNSlpHZVE5WHRPczNjTmV0bkJ4TlVKOGlFNkhzWHpfVG9rZW46U1hqemJwWGxnb0pXZll4MGkyTmN1VGRNbmlnXzE2OTA0NjM1ODY6MTY5MDQ2NzE4Nl9WNA) |
|  9   | **.fontWeight(.light)**                                   | 指定**字重**(字体细一点)                |                                                              |
|  10  | **var**                                                   | 定义后期**可变**的变量                  | `var redValue:Double`                                        |
|  11  | **let**                                                   | 定义后期**不可改变**的变量              |                                                              |
|  12  | **Int****()**                                             | 整数                                    | `Text("R: \(Int(redValue))")`                                |
|  13  | **Double**                                                | 双倍,是个很长的小数,也称浮点数          | `@State var redValue:Double`                                 |
|  14  | **@State**                                                | 变量可跟着改变                          |                                                              |
|  15  | **$**                                                     | 响应元素的变化,与变量相关联             | `Slider(value: $redValue)`                                   |
|  16  | **Color(red: , green: , blue: )**                         | 指定RGB颜色                             | `Color(red:redValue, green: greenValue, blue: blueValue    )    .edgesIgnoringSafeArea(.all)` |
|  17  | **.edgesIgnoringSafeArea(.all)**                          | 将“楼层”铺满整个屏幕                    |                                                              |

实现这么一个小小的功能,你已经学会了很多基础概念,是不是一下子就能看懂了?好家伙,Swift并没有那么难学嘛,甚至还有点好玩.

> You've learnt a lot of basic concepts to implement such a small feature, so it's easy to see how you can understand it? Well, Swift isn't that hard to learn, and it's even a bit of fun.

当然,**不管是学什么,实践才是最重要的**,文字有时无法传达那么准确,毕竟你我大脑中的“镜像神经元”比文字更早诞生,特别擅长模仿,**跟着做一遍往往比读万卷书学得更快,这学习效率嘎嘎好!** 

> Of course, no matter what you learn, practice is the most important, the text sometimes can not be conveyed so accurately, after all, you and my brain "mirror neuron" was born earlier than the text, especially good at imitation, follow the do it again often faster than reading thousands of books to learn, the learning efficiency of this quagga good! 

期待你的进步,我们下期见.

> I look forward to your progress. I'll see you in the next issue.

**鸣谢**

> Acknowledgements

本教程在编撰过程中得到了多方的大力支持.特此鸣谢:**爱梅** 给予的写作指导,不愧是常年写作的人,向她学习并在此由衷的表示感谢.

> This tutorial has been compiled with the support of many people. Acknowledgement: Aimee gave writing guidance, worthy of a person who writes all year round, to learn from her and would like to express my heartfelt thanks.

**标签**

> Tags

[Swift](https://kxv36hgn51.feishu.cn/wiki/GSFewSmhqizDXfksatCc7QQ6nid)[编程](https://kxv36hgn51.feishu.cn/wiki/wikcnGrTUbs5WbYYtM9qRhQyp6g)

参考文献

> References

[1] https://youtu.be/hHZOAYsyd8Y

[2] https://youtu.be/Z7sRXqBGAAk