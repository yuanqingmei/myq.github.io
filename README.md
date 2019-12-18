## Welcome to GitHub Pages

You can use the [editor on GitHub](https://github.com/yuanqingmei/myq.github.io/edit/master/README.md) to maintain and preview the content for your website in Markdown files.

Whenever you commit to this repository, GitHub Pages will run [Jekyll](https://jekyllrb.com/) to rebuild the pages in your site, from the content in your Markdown files.

### Markdown
20191218@nju.cs.712
python 字符串转列表出现\ufeff的解决方法

在学习python从文件中读取文件，并将文件中的字符串转化为列表的时候，发现文件头多了一个\ufeff字符。
　　这个问题前段时间也遇到过了，同样是上网搜索了半天才解决，当时只是把问题解决就过去了，但是今天遇到同样的问题时，知道有这么一个解决方法，但是怎么做就是想不起来。古人云，好记性不如烂笔头，一点没错。进入正题。
　　几个概念性的东西 　　
　　ANSCII: 
标准的 ANSCII 编码只使用7个比特来表示一个字符，因此最多编码128个字符。扩充的 ANSCII 使用8个比特来表示一个字符，最多也只能 
编码 256 个字符。 

　　UNICODE: 
使用2个甚至4个字节来编码一个字符，因此可以将世界上所有的字符进行统一编码。 

　　UTF: 
UNICODE编码转换格式，就是用来指导如何将 unicode 编码成适合文件存储和网络传输的字节序列的形式 (unicode -> 
str)。像其他的一些编码方式 gb2312, gb18030, big5 和 UTF 的作用是一样的，只是编码方式不同。 

在Windows下用文本编辑器创建的文本文件，如果选择以UTF-8等Unicode格式保存，会在文件头（第一个字符）加入一个BOM标识。
　　什么是BOM？
　　BOM = Byte Order Mark
　　BOM是Unicode规范中推荐的标记字节顺序的方法。比如说对于UTF-16，如果接收者收到的BOM是FEFF，表明这个字节流是Big-Endian的；如果收到FFFE，就表明这个字节流是Little-Endian的。
　　UTF-8不需要BOM来表明字节顺序，但可以用BOM来表明“我是UTF-8编码”。BOM的UTF-8编码是EF BB BF（用UltraEdit打开文本、切换到16进制可以看到）。所以如果接收者收到以EF BB BF开头的字节流，就知道这是UTF-8编码了。
具体方法请看下面代码


# filename: example.py
# conding=utf-8
f = open("news.txt", "r",encoding='utf-8')
file = f.read()
file_list = file.split(",")
print(file_list)
file_list2 = file.encode('utf-8').decode('utf-8-sig')
print(file_list2)

#打印结果如下
['\ufeff新华社北京2月8日电2月8日']
新华社北京2月8日电2月8日

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/yuanqingmei/myq.github.io/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://help.github.com/categories/github-pages-basics/) or [contact support](https://github.com/contact) and we’ll help you sort it out.
