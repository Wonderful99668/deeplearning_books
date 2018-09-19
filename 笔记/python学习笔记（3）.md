## python学习笔记（3）

### 一. I/O编程

__1. 读写文件__

读写模式:r只读,r+读写,w新建(会覆盖原有文件),a追加,b二进制文件

读写模式的类型有：

rU 或 Ua 以读方式打开, 同时提供通用换行符支持 

w     以写方式打开，
a     以追加模式打开 (从 EOF 开始, 必要时创建新文件)
r+     以读写模式打开
w+     以读写模式打开 (参见 w )
a+     以读写模式打开 (参见 a )
rb     以二进制读模式打开
wb     以二进制写模式打开 (参见 w )
ab     以二进制追加模式打开 (参见 a )
rb+    以二进制读写模式打开 (参见 r+ )
wb+    以二进制读写模式打开 (参见 w+ )
ab+    以二进制读写模式打开 (参见 a+ )

要读取非UTF-8编码的文本文件，需要给`open()`函数传入`encoding`参数，例如，读取GBK编码的文件：

```python
f = open('/Users/michael/gbk.txt', 'r', encoding='gbk')
```

遇到有些编码不规范的文件，你可能会遇到`UnicodeDecodeError`，因为在文本文件中可能夹杂了一些非法编码的字符。遇到这种情况，`open()`函数还接收一个`errors`参数，表示如果遇到编码错误后如何处理。最简单的方式是直接忽略：

```python
 f = open('/Users/michael/gbk.txt', 'r', encoding='gbk', errors='ignore')
```



由于文件读写时都有可能产生`IOError`，一旦出错，后面的`f.close()`就不会调用。所以，为了保证无论是否出错都能正确地关闭文件，我们可以使用`try ... finally`来实现：

```python
try:
    f = open('/path/to/file', 'r')
    print(f.read())
finally:
    if f:
        f.close()
```

可用`with`语句简化:

```python
with open('/path/to/file', 'r') as f:
    print(f.read())
```

当我们写文件时，操作系统往往不会立刻把数据写入磁盘，而是放到内存缓存起来，空闲的时候再慢慢写入。只有调用`close()`方法时，操作系统才保证把没有写入的数据全部写入磁盘。忘记调用`close()`的后果是数据可能只写了一部分到磁盘，剩下的丢失了。所以，还是用`with`语句来得保险：

```python
with open('/Users/michael/test.txt', 'w') as f:
    f.write('Hello, world!')
```

__2. 操作文件和目录__



###使用python创建数据库

impor PyMySQL
conn = MySQLdb.connect(host='localhost', user='root',passwd='')  
cursor = conn.cursor()
cursor.execute("""create database if not exists python""")
conn.select_db('python');
cursor.execute("""create table test(id int, info varchar(100)) """)
cursor.close(); 