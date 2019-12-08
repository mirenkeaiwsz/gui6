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

![lct](https://github.com/mirenkeaiwsz/gui6/blob/master/1575807375(1).png)

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

package xueshengxuanke;
import xueshengxuanke.*;
import javax.swing.*;

import java.awt.*;
import java.awt.event.*;
import java.io.File;
import java.io.FileInputStream;
import java.io.FileWriter;
import java.io.IOException;
public class GUI1 extends JFrame implements
ActionListener{  Cs cs;
                   Container c;
                   JLabel label1;JLabel label2;JLabel label3;JLabel label4,label5;JLabel label6;
               	JLabel label7;JLabel label8;JLabel label9;JLabel label10,label11;JLabel label12;JLabel label13;
               	JButton button1,button2;
               	
               	TextArea ta1;
               	JTextField t1,t2,t3,t4,t5,t6,t7,t8;
               	CheckboxGroup cbg;
               	               	JCheckBox c1,c2,c3;
               	
               	String bianhao[]={"004","005","006","007","008","009"};
               	String score[]={"0.5","1.0","1.5","2.0","2.5","3.0",
               			"3.5","4.0"};
               	public GUI1(){
               		super("选课系统");
               		label1=new JLabel("请输入个人信息和所选课程，完成后单击确定。            ");
               		label7=new JLabel("请输入开设的课程和信息，完成后单击确定。        ");
               		label2=new JLabel("学生姓名：");
               		
               		label3=new JLabel("性别:");
               		cbg = new CheckboxGroup(); 
               		
               		label6=new JLabel("学号：");
               		label4=new JLabel("生日：");
               		label5=new JLabel("课程：");
               		label11=new JLabel("上课地点：");

               	
               		c1=new JCheckBox("语文");
               		c2=new JCheckBox("数学");
               		c3=new JCheckBox("英语");
               		ta1=new TextArea(10,30);
               		
               		button1=new JButton("确定");
               		button2=new JButton("取消");
                                button3=new JButton("删除");
               		
               		t1=new JTextField("",5);
               		t2=new JTextField("",10);
               		t3=new JTextField("",5);
               		t4=new JTextField("",5);
               		t5=new JTextField("",5);
               		t6=new JTextField("",5);
               		t7=new JTextField("",5);
               		t8=new JTextField("",5);
               		setBounds(600,300,625,600);
               		try {UIManager.setLookAndFeel(UIManager.getSystemLookAndFeelClassName());
               		}catch(Exception e){}
               		c=getContentPane();	

               		c.setLayout(new FlowLayout(FlowLayout.LEFT));
               		c.add(label1);
               		
               		c.add(label2);
               		c.add(t1);

               		c.add(label3);
               		
               		c.add(new Checkbox("男", cbg, true)); 
               		c.add(new Checkbox("女", cbg, false));
               		
               		c.add(label6);
               		c.add(t2);

               		c.add(label5);
               		c.add(c1);c.add(c2);c.add(c3);
               		  		
               		c.add(ta1);
		
               		c.add(button1);
               		c.add(button2);
               		c.add(button3);               		
               		
               		setVisible(true);
               		button1.addActionListener(this);
               		button2.addActionListener(this);
               		
               		setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);

               		}
               	public void actionPerformed(ActionEvent e){
               		Cs p = null;
            		Cs q = null;
            		Cs r = null;
            		
            	    Student students = null;
            	    Cs cs;
            	    String str="";
            	    
            	    try {
            	    	File name1 = new File("D:\\课程.txt");
            	    	 FileInputStream in=new FileInputStream(name1);
            	    	 byte[] buffer=new byte[2048];
            	    	 in.read(buffer);
            	    	 in.close();
            	    	 
            	    	 str=new String(buffer);
            	    	
            	    } catch (IOException e1) {
            	    	// TODO Auto-generated catch block
            	    	e1.printStackTrace();
            	    } 
            	    String b[] = str.split(",");
                	p  = new Cs(b[0],b[1],b[2],b[3]);
                	q  = new Cs(b[4],b[5],b[6],b[7]);
                	r  = new Cs(b[8],b[9],b[10],b[11]);
                
               			if(e.getSource()==button1) {
               				
               				
               				ta1.append("姓名："+t1.getText()+"\n"+
               				"学号："+t2.getText()+"\n"+"性别："
               				+cbg.getSelectedCheckbox().getLabel()+
               				"\n");
               			byte[] se= new byte[4096];
               			StringBuffer st= new StringBuffer();
               				if(c1.isSelected() && e.getSource()==button1)
               					{ta1.append( "课程：" + c1.getLabel()+" "+p.toString()+"\n");
               					students = new Student(t1.getText(),t2.getText(),cbg.getSelectedCheckbox().getLabel(),p);
               					StringBuffer s1=new StringBuffer();
               					s1.append(students);
               					s1.append(p);
               					st.append(s1);}
               				if(c2.isSelected() && e.getSource()==button1) {
               					ta1.append( "课程：" + c2.getLabel()+" "+q.toString()+"\n");
               					students = new Student(t1.getText(),t2.getText(),cbg.getSelectedCheckbox().getLabel(),q);
               					StringBuffer s2=new StringBuffer();
               					
               					s2.append(q);
               					st.append(s2);}
               				if(c3.isSelected() && e.getSource()==button1) {
               					ta1.append( "课程：" + c3.getLabel()+" "+r.toString()+"\n");
               					students = new Student(t1.getText(),t2.getText(),cbg.getSelectedCheckbox().getLabel(),r);
               					StringBuffer s3=new StringBuffer();
               					
               					s3.append(r);
               					st.append(s3);
               					ta1.append("\n");}
               					try {
            						FileWriter fw=new FileWriter("D:\\选课信息.txt");
            						fw.write(st.toString());
            						fw.close();
            						} 
            					catch (IOException n) 
            						{
            						n.printStackTrace();
            						}}
               			
               			if(e.getSource()==button2){
               				System.exit(0);
               			}
               			
               				cs = new Cs(t4.getText(),t5.getText(),
               						t6.getText(),t7.getText());

               		}
               	
               	public static void main(String[] args){
               		GUI1 d = new GUI1();
               	}

}

七、程序截图
![]()
![]()
![]()
![]()
![]()
