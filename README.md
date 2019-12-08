一、实验目的

分析学生选课系统。使用GUI窗体及其组件设计窗体界面。完成学生选课过程业务逻辑编程。基于文件保存并读取数据。处理异常。

二、实验要求

1、
设计GUI窗体，支持学生注册、课程新加、学生选课、学生退课、打印学生选课列表等操作。

2、
基于事件模型对业务逻辑编程，实现在界面上支持上述操作。

3、
针对操作过程中可能会出现的各种异常，做异常处理

4、
基于输入/输出编程，支持学生、课程、教师等数据的读写操作。

5、
基于Github.com提交实验，包括实验SRC源文件夹程序，README.MD实验报告文档。

三、实验思路

首先一个完备的选课系统的GUI界面需要包括各种不同的输入方法，例如：选择，填入，按钮等，要充分利用不同的窗口组件建立这个界面窗口。所以在建了不同的组件之后就要给这些组件赋值。之后在容器中引用这些被赋值过的组件。作为一个选课系统首先要自己包含课程信息，所以我们新建立一个txt文件来事先储存这些课程的基本信息，例如课程名称，上课地点，学分，课程编号等。这些信息在我们使用程序时会被提取出来，应用。这时我们又需要另一个txt文件来储存这些已经选过课程的同学的信息。

四、流程图

![lct](https://github.com/mirenkeaiwsz/gui6/blob/master/1575804189(1).png)

五、部分函数的使用方法及注释

1.JTextField

SetText(string) 设置文本域中的文本值
GetText()返回文本域中的输入文本值
getColumns()返回文本域的列数
setEditable(Boolean) 设置文本域是否为只读状态

JTextField() 构造一个新的 TextField。
JTextField(int columns) 构造一个具有指定列数的新的空 TextField。
JTextField(String text) 构造一个用指定文本初始化的新TextField。
JTextField(String text, int columns) 构造一个用指定文本和列初始化的新TextField。

2.ActionListener

如当用户点击按钮或选择菜单项目时，Swing组件会产生一个 ActionEvent。Swing组件会产生许多事件，如ActionEvents,ChangeEvents,ItemEvents等，来响应用户的鼠标点击行为，列表框中值的改变，计时器的开始计时等行为。在Java Swing编程中，通过注册监听器，我们可以监听事件源产生的事件，从而在事件处 理程序中处理我们所需要处理的用户行为。当特定于组件的动作（比如被按下）发生时，由组件（比如 Button）生成此高级别事件。事件被传递给每一个ActionListener 对象，这些对象是使用组件的addActionListener 方法注册的，用以接收这类事件。
public interface ActionListener
extends EventListener
用于接收操作事件的侦听器接口。
方法只有一个：
actionPerformed
void actionPerformed(ActionEvent e)
发生操作时调用。

3.setVisible

setVisible(true);方法的意思是说数据模型已经构造好了，允许JVM可以根据数据模型执行paint方法开始画图并显示到屏幕上了，并不是显示图形，而是可以运行开始画图了， 这个方法和java多线程的start方法有点异曲同工之妙，start方式是允许run方法运行了，start方法和setVisible方法很相似。
但为了安全起见，还是要把setVisible()方法放到最后面。代码是按顺序执行的 ，如果把setVisible()放在前边，后边再添加其他组件的时候，有可能不会显示出来。

4.actionPerformed

public void actionPerformed(ActionEvent e)
这是接口ActionListener里面定义的一个抽象方法，所有实现这个接口的类都要重写这个方法。
一般情况下，这是在编写GUI程序时，组件发生“有意义”的事件时会调用这个方法，比如按钮被按下，文本框内输入回车时都会触发这个事件，然后调用你编写的事件处理程序。
实现过程大体如下：编写一个ActionListener类的侦听器，组件注册该侦听器，侦听器内部要编写这个actionPerformed方法。

六、部分代码
