# AMS实验记录
## 思考的一些问题
+ 查询卡时，利用数组或链表保存数据的迭代中，card_service()文件中将接受到的卡信息保存至数组或链表中，程序关闭后数组中数据被清除，再打开如何查询？
  + 解：将添加卡信息存入文件，之后读取文件信息至数组或链表
+ 如何将文件中数据写入数组或链表中？
  + 解：使用循环以及fread（）函数；例：
  ```c
    FILE* fp;
	fp = fopen(PATH, "rb");//打开文件
	if (fp == NULL)
	{
		printf("文件打开失败！");
		exit(0);
	}
	pList_card head = NULL, p = NULL;
	head = make();
	Card tool_card, goal_card;
	while (1)
	{
		if (fread(&tool_card, sizeof(Card), 1, fp) == 0)//读取文件信息至结构体
		{
			break;
		}
		head = add_message(head, tool_card);//将结构体信息存入链表
	}
	fclose(fp);//关闭文件
	```
+ 如何根据卡号找到文件中对应信息并显示？
  + 解：将文件中信息全部读入链表中，再在链表中查找对应信息结点
+ 在函数中定义一个结构体变量，在里面存入信息后，该函数返回结构体变量的地址，那么调用该函数时如何得到结构体中信息？
  + 解：注意使用“*”
+ 如何查找一个字符串中是否包含另一个字符串（用于模糊查找）？
  + 解：开始时想要写一个函数，之后发现strstr（）函数有此功能
  + char* strstr(const char *s1,const char *s2);//判断s2是否为s1子串
+ 如何将一个time_t类型的变量转化为格式化时间的形式？
  + 使用strftime（）函数与localtime（）函数
  ```c
  time_t nowtime=time(NULL);//当前时间
  char str[50], *format = "%Y-%m-%d %H:%M:%S";
  strftime(str, sizeof(str), format, localtime(&nowtime));
  printf("%s",str);//显示格式化的时间
  ```
+ 如何将文件中储存的卡信息进行更新？
  + 将文件中所有信息写入链表中，对链表进行修改，再将链表写入文件
+ 保存文件时，save_card(const void* pcard,const char* ppath,const char* made);
向文件写入信息时，fwrite(pcard,sizeof(?),1,fp);写入字节大小由pcard类型而定，当类型不同时如何表示写入字节的大小？
  + 解：重新写一个函数保存对应类型数据；
+ 如何更改c语言窗口的背景颜色与字体颜色?
  + 加入#include<stdlib.h>头文件；
  + 调用system("color xx");xx分别指的是背景颜色和文字颜色，x为一位16进制数（1-f），可以随意组合；
  + 注：0：黑色、1：蓝色、2：绿色、3：湖蓝色、4：红色、5：紫色、6：黄色、7：白色、8：灰色、9：淡蓝色、a：淡绿色、b：淡浅绿色、c：淡红色、d：淡紫色、e：淡黄色、f：亮白色；
+ 如何实现输入密码时的保密？
  + 注意输入时使用getch（）函数使输入字符不在屏幕上显示；
  + 输入密码前有输入的卡号时，使用getchar();来读取前面输入结束时的回车；
  + "\r"为回车，"\n"为换行；
 ```c
 char* protect_pwd()//密码保护
 {
	char cardpwd[20]={'\0'};
	char tool = '\0';
	int i = 0;
	while (1)
	{
		tool = getch();
		if (tool == '\r')
			break;
		cardpwd[i] = tool;
		putchar('*');
		i++;
	}
	printf("\n");
	return cardpwd;
 }
 char card_pwd[20],*ppwd=NULL;
 printf("请输入上机密码（长度1~8）：");
 ppwd = protect_pwd();//密码保护
 strcpy(card_pwd, ppwd);
 ppwd = card_pwd;
```


## 程序运行后报错问题及所犯低级错误
+ 写的将时间（time_t类型）转化为对应时间字符串的函数char* str_time(const time_t* ptime);引发异常
  + 解：其中所用的strcat（）函数一直报错，之后使用库函数中的strftime（）
  + size_t strftime(char *str,size_t count,const char *format,const struct tm *tm);
  ```c
  void message2_card(const Card* pcard)//显示查询卡信息
  {
	char str[50], * format = "%Y-%m-%d %H:%M:%S";
	strftime(str, sizeof(str), format, localtime(&pcard->tLast));
	printf("卡号\t状态\t余额\t累计使用\t使用次数\t上次使用时间\n");
	printf("%s\t%d\t%.1f\t%.1f\t\t%d\t\t%s\n", pcard->aName, pcard->nStatus, pcard->fBalance, pcard->fTotalUse, pcard->nUseCount, str);
  }
  ```
+ 使用制表符“\t”时，上下两行信息没对齐
  + 解：多写一个“\t”；在\t之前的字符少于8n（n=1.2.3…n）个空格（8个空格就是一个tab），自动补全8个空格；在\t之前的字符多于8n（n=1.2.3…n）个空格,自动补一个8个空格
+ fopen（）后忘记fclose（）
+ 链表读取文件信息时，显示信息时出错
  + 向message2_card(const Card* pcard);中传入一个指针时出错，传入一个地址正确；
+ 遍历输出卡信息时，disp_list();忘记将结点指针p=p->next,造成死循环
+ 选择菜单编号时，输入数字时正常，输入但输入字符时会异常死循环
+ 组合文件保存路径的字符串时，strcat一直异常
  + 使用指针只有地址，使用时由于没有申请内存大小，可能发生冲突
+ 链表使用完后，总会忘记释放链表
+ 保存信息至文件时，函数中传入的指针类型有多种时，用void*
+ switch...case...中报错：声明不能包含标签
  + 在case语句后加上{}
+ PCH 警告: 头停止点不在文件范围内。未生成 IntelliSense PCH 文件。
  + 查找的解决方法：在VS中依次单击：工具–选项–文本编辑器–C/C++–高级–禁用 IntelliSence，将“false”改为“true”。
  + 结果没用，后来发现在函数声明的头文件中最后一个函数声明没有加“；”
+ 当使用一个char类型的指针char *p时，同时有一个字符数组char str[100];使指针指向字符数组p=&str,在调用函数时，形参类型为char\*时写入p会读不进str中的数据
+ 使一个字符型指针指向一个字符串，要将其写入字符数组时，char str[100]=*pstr,会报错：初始化需要带括号的表达式列表；
如果定义后写str[100]=*pstr,会报错字符数组溢出，且无论字符数组定义多大都会显示溢出；
  + 如果加上{}，char str[100]={*pstr};只能写入pstr所指的首个字符；
  + 可以使用strcpy()函数进行复制，strcpy(str,pstr);
+ 下机时，将卡保存至单独文件时，使用函数save_card(pcard,pathcard,"a");使用完后pcard中数据丢失aName与aPwd;
+ 选择菜单编号时，当输入错误时，输错数字会正常有选择错误的提示；但是有时若输入一个字符串时，会出不同的错误，有时是胡乱运行菜单功能中的代码，有时是死循环；
  + 选择菜单编号时scanf中将%d换为%s，再将字符串通过atio()函数转换为数字，同时将退出时的数字由0换位10；
  + 原型：int atoi(const char *nptr);
  + 说明：参数nptr字符串，如果 第一个非空格字符存在，是数字或者正负号则开始做类型转换，之后检测到非数字(包括结束符 \0) 字符时停止转换，返回整型数；否则，返回零。
  ```c
    char str[20];
	int select_num = -1;
	do
	{
		//菜单页面输出
		outputMenu(); 
		//输入选择菜单编号
		scanf("%s",str);
		select_num = atoi(str);
		//输出所选菜单项
		output_selectnum(select_num);
	} while (select_num != 10);
  ```