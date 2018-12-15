
=================
color configuration
tag: PS1colorconfiguration

格式: echo -e "\033[格式化属性;字体颜色;背景颜色m字符串\033[0m"  attention: 顺序其实不影响实际配置

	\033=\e=\x1B
 
	 PS1='\[\e[1;33m\][\d \t \u@\h \w]\$\[\e[m\] '
	 
	 PS1="\[\e[37;40m\][\[\e[31;40m\]\t \[\e[32;40m\]\u\[\e[37;40m\]@\h \[\e[36;40m\]\w\[\e[0m\]]\\$ "
例如: echo -e "\033[41;36m something here \033[0m"  其中41的位置代表底色, 36的位置是代表字的颜色  
那些ascii code 是对颜色调用的始末.  \033[ ; m …… \033[0m  
字背景颜色范围:40----49  40:黑  41:深红  42:绿  43:黄色  44:蓝色  45:紫色  46:深绿  47:白色  
字颜色:30-----------39  30:黑  31:红  32:绿  33:黄  34:蓝色  35:紫色  36:深绿  37:白色  
ANSI控制码的说明  
	\33[0m 关闭所有属性  
	\33[1m 设置高亮度  
	\33[4m 下划线  
	\33[5m 闪烁  
	\33[7m 反显  
	\33[8m 消隐  
	\33[30m -- 
	\33[37m 设置前景色  
	\33[40m -- 
	\33[47m 设置背景色  
	\33[nA 光标上移n行  
	\33[nB 光标下移n行  
	\33[nC 光标右移n行  
	\33[nD 光标左移n行  
	\33[y;xH设置光标位置  
	\33[2J 清屏  
	\33[K 清除从光标到行尾的内容  
	\33[s 保存光标位置  
	\33[u 恢复光标位置  
	\33[?25l 隐藏光标  
	\33[?25h 显示光标
	
-------------------
Introduction

Your shell can be personalized quite a lot. Using settings in your .bashrc file you can change the prompt, set up aliases and much more.
Activating changes

Once you have edited your .bashrc file you will want to activate the changes without logging out and back in again. Use
source ~/.bashrc
to do this.
The prompt

The standard prompt is a pretty boring and basic item. You can make it more useful by configuring it to display information you need and change the colors to make it stand out.

If you do most of your work on the bash prompt as a normal user but occasionally
su
to root, it is nice to have a clear indication that you are root. One way to do this is to set the color of the prompt to be green for a normal user and red for root. To do this you need to edit the two .bashrc files: ~/.bashrc and /root/.bashrc
In your ~/.bashrc file add this line:

PS1='\[\e[1;32m\][\u@\h \W]\$\[\e[0m\] '

In your /root/.bashrc add this line

PS1='\[\e[1;31m\][\u@\h \W]\$\[\e[0m\] '

The first part
\[\e[1;32m\]
and
\[\e[1;31m\]
sets the color. The last part
\[\e[0m\]
returns the color to white. The bits in between
[\u@\h \W]\$
are what give you the information
username @ hostname
.

In this ANSI color code,
\[\e[1;32m\]
, the ANSI color codes are the bits inside the inner brackets:
1;32m
. If there is a semicolon,
;
, then the first part is the modifier and the second part is the color. In this case the 1 means bold. The colors can be any of these:

30 = Black
31 = Red
32 = Green
33 = Yellow
34 = Blue
35 = Magenta
36 = Cyan
37 = White

If you just wanted normal red you would use
31m
instead of
1;31m
. To reset the color back to default you use
0m
.

The individual parts are as follows
\u – Username.
\h – Hostname.
\w – Current absolute path. Use \W for current relative path.
\$ – The prompt character This will be # for user root, $ for regular users).

There are lots of other escape codes you can use in your prompt. To find out more please see
man bash