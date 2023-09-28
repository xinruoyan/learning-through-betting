# 《Python编程从入门到实践》学习笔记(异常)

## 
学习处理异常可以帮助我们应对文件不存在等情况，以及处理其它可能导致程序崩溃的问题。

### 什么是异常
Python使用成为异常（exception)的特殊对象来管理程序执行期间发生的错误。每当发生让Python不知所措的错误时，它都会创建一个异常对象。如果你编写了处理该异常的代码，程序将继续运行；如果你未对异常进行处理，程序将停止，并显示一个traceback,其中包含有关异常的报告。

### 怎么看异常

要看懂复杂的traceback，通常最好从traceback的末尾开始看。

### 如何处理异常

#### 1）使用try-except代码块
预测可能发生何种错误，然后把它放在try-except代码块中，并告诉Python如何应对。

e.g. 处理ZeroDivisionError异常的try-except代码块类似于这样：

try:

    answer = int(first_number) / int(second_number)
	
except ZeroDivisionError:

    print("You can't divide by zero!")

#### 2）使用else代码块

只有try代码块成功执行才需要继续执行的代码，都应该放在else代码块中, e.g.

try:

    answer = int(first_number) / int(second_number)
	
except ZeroDivisionError:

    print("You can't divide by zero!")
	
else:

    print(answer)

### 常见异常 FileNotFoundError

在使用文件时，要查找的文件可能在其它地方，文件名可能不正确，或者文件根本就不存在，都会导致Python找不到文件，从而引发异常FileNotFoundError。可以运行except代码块中的代码，或者显示一条友好的错误信息，或者直接用占位符Pass进行静默处理。Python的错误处理结构能让我们决定与用户共享错误信息的程度。

### 注意

让用户看到traceback，有时候不是个好主意。它有可能会让不懂技术的用户发晕，或者被怀有恶意的用户追踪到你不想让他们知道的信息。