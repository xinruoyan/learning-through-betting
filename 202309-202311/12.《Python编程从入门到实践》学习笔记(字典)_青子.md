# 《Python编程从入门到实践》学习笔记(字典)
## 1. 什么是字典
在python中，字典（dictionary)是一系列键值对。每个键都与一个值关联，可以使用键来访问与之关联的值。而与键相关联的值可以是数、字符串、列表乃至字典。字典中可包含任意数量的键值对。

字典用放在花括号（{}）中的一系列键值对表示，当你指定键时，python将返回与之关联的值。键和值之间用冒号分隔，而键值对之间用逗号分隔。比如
alien={'color':'green', 'points':5}

## 2. 常见的字典操作
### 2.1 创建一个空字典
如果要使用字典来存储用户提供的数据或者编写能自动生成大量键值对的代码，通常需要先定义一个空字典。
先用一对花括号定义一个空字典，再分行添加各个键值对。
字典alien={'color':'green', 'points':5}的创建过程可以是这样的：
alien={}
alien['color']='green'
alien['points']=5
print(alien)

### 2.2 访问字典中的值
要获取与键关联的值，可指定字典名并把键放在后面的方括号内，比如要打印alien中points：
alien={'color':'green', 'points':5}
print(alien['points'])
出来的结果是5。

另外，还可以使用get()来访问字典的值。get()方法的第一个参数用于指定键，是必不可少的；第二个参数为当指定的键不存在时要返回的值，是可选的。

### 2.3 添加键值对
字典是一种动态结构，可随时在其中添加键值对。要添加键值对，可依次指定字典名、用方括号括起来的键和与该键关联的值。
字典会保留定义时的元素排列顺序。如果将字典打印出来或遍历其元素，将发现元素的排列顺序与其添加顺序相同。
alien={'color':'green', 'points':5}
在字典alien中添加两项信息：外星人的x坐标和y坐标
alien['x_position']=0
alien['y_position']=25
print(alien)，显示结果如下：
alien={'color':'green', 'points':5，'x_position':0, 'y_position':25}

### 2.4 修改字典中的值
要修改字典中的值，可依次指定字典名、用方括号括起来的键和与该键关联的新值。
alien={'color':'green'}
print(f'The alien is {alien['color']}.'),显示结果为The alien is green.
alien['color']='yellow'
print(f'The alien is now {alien['color']}.'),显示结果为The alien is now yellow.

### 2.5 删除键值对
可使用del语句将字典中不再需要的信息的键值对彻底删除。在使用del语句时，必须指定字典名和要删除的键。
比如，从字典alien中删除键'color'及其值：
alien={'color':'green', 'points':5}
print(alien),显示结果为{'color':'green', 'points':5}
del alien['color'], 删除color
print(alien), 显示的结果为{'points':5}