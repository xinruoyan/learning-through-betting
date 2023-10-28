# 《Python编程从入门到实践》学习笔记(文件)

## 1. 读取文件
要使用文本文件中的信息，首先需要将信息读取到内存中。既可以一次性读取文件的全部内容，也可以逐行读取。要使用文件的内容，需要将其路径告知Python。路径（path)指的是文件或文件夹在系统中的准确位置。在编程中，指定路径的方式有两种：相对路径和绝对路径。

相对路径让Python到相对于当前运行的程序所在目录的指定位置去查找。
path=Path(text_files/filename.txt')

绝对路径以系统的根文件夹为起点。
path=Path('/home/eric/data_files/text_files/filename.txt')

### 读取文件的全部内容
Python提供了Pathlib模块，让我们能够更轻松地在各种操作系统中处理文件和目录。
e.g.
from pathlib import Path
path=Path('pi_digits.txt')
contents=path.read_text()
print(contents)

创建文件地Path对象后，使用read_text()方法来读取这个文件的全部内容。read_text()将该文件的全部内容作为一个字符串返回，而我们将这个字符串赋给了变量content。打印contents的值时，将显示这个文本文件的全部内容。

read_text()在到达文件末尾时会返回一个空字符串，而这个空字符串会被显示为一个空行。

要在读取文件内容时删除末尾的换行符，可在调用read_text()后直接调用方法rstrip():
contents=path.read_text().rstrip()

### 访问文件中的各行
splitlines()方法返回一个列表，其中包含文件中所有的行，我们将这个列表赋给变量Lines。使用splitlines()方法将冗长的字符串转换为一系列行，再使用for循环以每次一行的方式检查文件中的各行：
from pathlib import Path
path=Path('pi_digits.txt')
conents=path.read_text()
lines=contents.splitlines()
for line in lines:
    print(line)

在读取文本文件时，Python将其中的所有文本都解释为字符串。如果读取的是数，并且要将其作为数值使用，就必须使用int()函数将其转换为整数，或者使用float()函数将其转换为浮点数。

## 2.写入文件
保存数据的最简单的方式之一就是将其写入文件。通过将输出写入文件，即便关闭包含程序输出的终端窗口，这些输出依然存在。Python只能将字符串写入文本文件。如果要将数值数据存储到文本文件中，必须先使用函数str()将其转换为字符串格式。

### 写入一行
定义一个文件的路径后，用write_text()将数据写入该文件。
from pathlib import Path
path=Path('programming.txt')
path.write_text("我喜欢Python") 打开programming文件能看到一句话：我喜欢Python

### 写入多行
要写入多行，需要先创建包含要写入文件的全部内容的字符串，再调用write_text()并将这个字符串传递给它。
首先定义变量contents，用于存储要写入文件的所有内容。接着，用运算符+=在该变量中追加这个字符串，在每行末尾都添加换行符，让每个句子都各占一行。
from pathlib import Path
contents="我想学编程。\n"
contents+="我想先学Python。\n"
contents+="我现在在看蟒蛇书。\n"
path=Path('programming.txt')
path.write_text(contents)

注意：在对path对象调用write_text()方法时，务必谨慎。如果指定的文件已经存在，write_text()将删除其内容，并将指定的内容写入其中。