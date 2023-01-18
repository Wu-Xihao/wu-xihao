# AMS实验说明以及代码
## 说明
+ 由于读写文件掌握不好，所以将卡信息存入文件后所见为乱码，但不影响程序运行；
+ AMS的文件夹处于我的电脑上的D盘，读写文件的路径都是特定的，只确保在我的电脑上正常运行；
+ 在写代码时我并未完全按照电子书上的要求去写，只是阅读所需功能后自己去写代码；
+ 写代码时我将大部分函数写入card_service.c文件中，少量写入menu.c与manage.c文件中，所有的函数声明以及所有结构体定义位于service.h文件中，代码存放文件有些乱；
+ card_service.c文件中的函数是将菜单中的各个功能所需函数放在一起；并未根据电子书上所列结构将函数按找不同用途放入不同.c文件中；
+ 本次写代码时总是走一步算一步，导致有好的想法时，发现前面所写代码有许多可以优化，但是由于代码之间的关联性，不敢进行随意改动，所以代码有很多地方的不足；
+ 选择菜单时，要先选择编号9添加一个管理员后再制定消费规则，然后在上机与下机时才能正确计费；
+ 菜单中的管理与其它8个菜单选项分别为管理员层面与使用者层面，在菜单中将它们放在一起，此处仍有不足；
+ 代码中并未添加根据时间段来查询消费记录的功能；

## 代码
+ main.c文件
```c
#pragma warning(disable:4996)
#define _CRT_SECURE_NO_WARNINGS
#include<stdio.h>
#include<stdlib.h>
#include"menu.h"

int main()
{
	printf("欢迎进入计费管理系统！\n\n");
	char str[20];
	int select_num = -1;
	do
	{
		//界面颜色
		system("color 1f");
		//菜单页面输出
		outputMenu(); 
		//输入选择菜单编号
		scanf("%s",str);
		select_num = atoi(str);
		//输出所选菜单项
		output_selectnum(select_num);
		
	} while (select_num != 10);
	return 0;
}
```
+ menu.c文件
```c
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>
#include<stdlib.h>
#include<string.h>
#include<time.h>
#include"menu.h"
#include"service.h"
#define PATH "D:\\AMS\\AccountManagement\\data\\card_data.txt"
#define NUM 100
//输出菜单
void outputMenu()
{
	//int select_num = -1;
	printf("-----菜单-----\n");
	printf("1.添加卡\n2.查询卡\n3.注销卡\n");
	printf("4.上机\n5.下机\n");
	printf("6.充值\n7.退费\n8.消费记录查询\n");
	printf("9.管理\n10.退出\n");
	printf("请输入所选菜单编号数字(1~10):");
}
//输出所选菜单编号
void output_selectnum(int select_num)
{
	switch (select_num)
	{
	case 1:
		printf("-----添加卡-----\n");
		add();
		break;
	case 2:
		printf("-----查询卡-----\n");
		query();
		break;
	case 3:
		printf("-----注销卡-----\n");
		annul();
		break;
	case 4:
		printf("-----上机-----\n");
		logon();
		break;
	case 5:
		printf("-----下机-----\n");
		settle();
		break;
	case 6:
		printf("-----充值-----\n");
		addMoney();
		break;
	case 7:
		printf("-----退费-----\n");
		refundMoney();
		break;
	case 8:
		printf("---消费记录查询---\n");
		billRecord();
		break;
	case 9:
		printf("-----管理-----\n");
		manage();
		break;
	case 10:
		printf("退出\n");
		break;
	default:
		printf("输入的菜单序号错误！\n"); 
	}
	printf("\n");
}
//添加卡
void add()
{
	Card card;
	input_card(&card);
	int num1 = save_card(&card, PATH, "a");//将卡存入文件（该文件包含所有卡）
	char *pathcard=NULL;
	char path[100];
	strcpy(path, path_card(card.aName));
	pathcard = path;
	int num2 = save_card(&card, pathcard, "a");//将添加的卡再独立存入一个文件
	int sign = money_status(card.aName, card.fBalance, 0);//将开卡金额信息存入消费记录所在文件
	if (sign == 0)
		printf("开卡金额信息存入文件失败！\n");
	else
	{
		if (num1 == 0 || num2 == 0)
			printf("添加卡失败！\n");
		else
			printf("添加卡成功！\n");
		message1_card(&card);
	}
	system("pause");
}
//查询卡
void query()
{
	extern Card aCard[NUM];
	char card_name[50],*pstr;
	printf("请输入查询的卡号（长度1~18）：");
	scanf("%s", card_name);
	pstr = card_name;
	//使用结构体查找
	/*int cardnum = queryCard1(pstr);
	if (cardnum==-1)
		printf("没有该卡信息！");
	else
	message2_card(&aCard[cardnum]);*/
	//使用链表准确查找
	/*Card target_card;
	target_card = *queryCard(pstr);
	if(queryCard(pstr) ==NULL)
		printf("没有该卡信息！");
	else
		message2_card(&target_card);*/
	//使用链表模糊查找
	int num = 0;
	pList_card goal_head = queryCards(pstr, &num);
	if (goal_head->next == NULL)
		printf("没有该卡信息！\n");
	else
		disp_list(goal_head);
	release_cardList(goal_head);
	system("pause");
}
//注销卡
void annul()
{
	int sign = do_annul();
	if (sign == 0)
		printf("注销卡失败！\n");
	system("pause");
}
//上机
void logon()
{
	char card_name[50],card_pwd[20], *pstr1=NULL,*pstr2=NULL;
	printf("请输入上机卡号（长度1~18）：");
	scanf("%s", card_name);
	pstr1 = card_name;
	printf("请输入上机密码（长度1~8）：");
	//scanf("%s", card_pwd);
	getchar();//接收回车键
	pstr2 = protect_pwd();//密码保护
	strcpy(card_pwd, pstr2);
	pstr2 = card_pwd;
	printf("---上机信息如下---\n");
	Card goal_card, * pcard = NULL;
	pcard=do_logon(pstr1,pstr2);//上机验证
	if (pcard == NULL)
		printf("上机失败！\n");
	else if (pcard->nStatus != 0)//状态
		printf("上机失败！\n");
	else if (pcard->fBalance <= 0)//余额
		printf("上机失败！\n");
	else
	{
		pcard->nStatus = 1;
		goal_card = *pcard;
		Rule *prule= bill_message();//消费类型选择
		Rule bill_rule;
		bill_rule = *prule;
		int sign= bill_addto_file(&bill_rule, goal_card);//计费信息保存至文件
		if (sign == 0)
			printf("计费信息保存失败！\n");
		else
		{
			char* pathcard = NULL;
			char path[100];
			strcpy(path, path_card(goal_card.aName));//单独文件路径
			pathcard = path;
			int num = save_card(&goal_card, pathcard, "a");//添加上机信息至卡的单独文件
			if (num == 0)
				printf("更新信息失败！\n");

			pList_card head = update_file(&goal_card);//将文件信息存入链表，对链表更新信息，再重新写入文件
			if (head == NULL)
			{
				printf("文件更新失败！\n");
			}
			else
				release_cardList(head);
			message4_card(&goal_card);//上机显示卡信息
		}
	}
	system("pause");
}
//下机
void settle()
{
	char card_name[50], card_pwd[20], * pstr1, * pstr2;
	float money=0,bill_money=0;//用于记录消费金额
	printf("请输入下机卡号（长度1~18）：");
	scanf("%s", card_name);
	pstr1 = card_name;
	printf("请输入下机密码（长度1~8）：");
	//scanf("%s", card_pwd);
	getchar();//接收回车键
	pstr2 = protect_pwd();//密码保护
	strcpy(card_pwd, pstr2);
	pstr2 = card_pwd;
	printf("---下机信息如下---\n");
	Card *pcard = NULL;
	pcard = do_settle(pstr1, pstr2,&money);
	//bill_money = money;
	if (pcard == NULL)
		printf("下机失败！\n");
	else
	{
		char* pathcard = NULL;
		char path[100];
		Card goal_card = *pcard;//由于下面save_card（）后pcard数据丢失卡名密码，所以令goal_card保存数据
		strcpy(path, path_card(pcard->aName));//单独文件路径
		pathcard = path;
		int num = save_card(pcard, pathcard, "a");//添加下机信息至卡的单独文件
		if (num == 0)
			printf("更新信息失败！\n");
		pList_card head = NULL;
		head = update_file(&goal_card);//更新所有卡所在文件中该卡的信息
		if (head == NULL)
		{
			printf("文件更新失败！\n");
		}
		else
			release_cardList(head);

		message5_card(&goal_card,money);//显示下机信息
	}
	system("pause");
}
//充值
void addMoney()
{
	int sign = do_addmoney();
	if (sign == 0)
		printf("充值失败！\n");
	system("pause");
}
//退费
void refundMoney()
{
	int sign = do_refundmoney();
	if (sign == 0)
		printf("退费失败！\n");
	system("pause");
}
//消费记录
void billRecord()
{
	int sign = do_billrecord();
	if (sign == 0)
		printf("消费记录查询失败！\n");
	system("pause");
}
//管理
void manage()
{
	int num = -1;
	printf("1.添加管理员\n2.修改计费标准\n3.查看营业额\n请选择编号：");
	scanf("%d", &num);
	switch (num) 
	{
	case 1:
		add_manager();
		break;
	case 2:
	{
		char manager_name[50], manager_pwd[20], * pname, * ppwd;
		printf("请输入管理员名：");
		scanf("%s", manager_name);
		pname = manager_name;
		printf("请输入密码：");
		//scanf("%s", manager_pwd);
		getchar();//接收回车键
		ppwd = protect_pwd();//密码保护
		strcpy(manager_pwd, ppwd);
		ppwd = manager_pwd;
		int sign = do_manage(pname, ppwd);
		if (sign == 0)
		{
			printf("错误！");
		}
		break;
	}
	case 3:
	{
		char manager_name[50], manager_pwd[20], * pname, * ppwd;
		printf("请输入管理员名：");
		scanf("%s", manager_name);
		pname = manager_name;
		printf("请输入密码：");
		//scanf("%s", manager_pwd);
		getchar();//接收回车键
		ppwd = protect_pwd();//密码保护
		strcpy(manager_pwd, ppwd);
		ppwd = manager_pwd;
		int sign = view_turnover(pname, ppwd);//查看营业总额
		if (sign == 0)
		{
			printf("查看失败！");
		}
		break;
	}
	default:
		printf("输入编号错误！");
	}
	system("pause");
}
```
+ card_service.c文件
```c
#pragma warning(disable:4996)
#define _CRT_SECURE_NO_WARNINGS
#pragma once
#include<stdio.h>
#include<stdlib.h>
#include<string.h>
#include<time.h>
#include"service.h"
#define PATH "D:\\AMS\\AccountManagement\\data\\card_data.txt"//卡信息路径
#define ALLBILL_PATH "D:\\AMS\\AccountManagement\\billing_file\\bill_message\\allbill_rule.txt"//计费标准信息保存路径
#define TURNOVER_PATH "D:\\AMS\\AccountManagement\\billing_file\\bill_message\\turnover.txt"//营业总额文件路径
#define NUM 100
extern Card aCard[NUM]={0};
//添加卡
void input_card(Card* card)//输入开卡信息
{
	char aName1[50] = { 0 }, aPwd1[20] = { 0 };
	struct tm* tStart1, * tEnd1;
	int sign = 0;
	printf("请输入卡号（长度1~18）：");//输入卡号并判断
	do
	{
		scanf("%s", aName1);
		if (strlen(aName1) > 18)
			printf("输入错误！\n请重新输入：");
		else {
			strcpy(card->aName, aName1);
			sign = 1;
		}
	} while (sign == 0);
	sign = 0;
	printf("请输入密码（长度1~8）：");//输入密码并判断
	do
	{
		scanf("%s", aPwd1);
		if (strlen(aPwd1) > 8)
			printf("输入错误！\n请重新输入：");
		else {
			strcpy(card->aPwd, aPwd1);
			sign = 1;
		}
	} while (sign == 0);
	printf("请输入开卡金额：");
	scanf("%f", &card->fBalance);
	card->fTotalUse = card->fBalance;
	card->nStatus = card->nUseCount = card->nDel = 0;
	card->tStart = card->tEnd = card->tLast = time(NULL);//时间处理
	tStart1 = tEnd1 = localtime(&card->tStart);
	tEnd1->tm_year = tStart1->tm_year + 1;
	card->tEnd = mktime(tEnd1);
}
char* path_card(const char* pname)//单独文件所有更新信息路径名
{
	char* path_card = NULL;
	char str1[100] = "D:\\AMS\\AccountManagement\\data\\all_update_message\\", * str2 = ".txt";
	strcat(str1, pname);
	strcat(str1, str2);
	path_card = str1;
	return path_card;
}
void message1_card(const Card* p_card)//显示开卡后的信息
{
	printf("---添加卡信息如下---\n");
	printf("卡号\t密码\t状态\t开卡金额\n");
	printf("%s\t%s\t%d\t%.2f\n", p_card->aName, p_card->aPwd, p_card->nStatus, p_card->fBalance);
}
//查询卡
pList_card make()//制作一个空链表
{
	pList_card head = NULL;
	pList_card tail = NULL;
	head = (pList_card)malloc(sizeof(List_card));
	if (head == NULL)
		return NULL;//头结点申请内存失败,返回NULL
	head->next = NULL;
	tail = head;
	return head;
}
pList_card add_message(pList_card head,Card message_card)//传入链表头指针，card中信息（值传递）
{
	pList_card p1=head,add=NULL;
	add = (pList_card)malloc(sizeof(List_card));
	add->card = message_card;
	add->next = NULL;
	while (p1->next != NULL)
	{
		p1 = p1->next;
	}
	p1->next = add;
	return head;
}
pList_card search_card(pList_card head, const char* pName)//寻找目标结点，返回结点指针，找不到返回NULL
{
	pList_card p = head;
	int sign = 0;
	while (p->next != NULL)//遍历链表
	{
		p = p->next;
		if (strcmp(&p->card.aName, pName) == 0)//判断卡名
		{
			sign = 1;
			break;
		}
	}
	if (sign == 0)
		return NULL;
	else return p;
}
pList_card search_cards(pList_card head, const char* pName,int* pIndex)//模糊查找，返回新建链表头结点指针，找不到返回NULL
{
	pList_card p = head,goal_head=NULL;
	goal_head = make();
	while (p->next != NULL)//遍历链表
	{
		p = p->next;
		if (strstr(&p->card.aName,pName) != NULL)//判断是否有关键字
		{
			(*pIndex)++;
			goal_head = add_message(goal_head, p->card);
		}
	}
	return goal_head;
}
void message2_card(const Card* pcard)//显示查询卡信息
{
	//printf("---查询卡信息如下---");
	char str[50], * format = "%Y-%m-%d %H:%M:%S";
	strftime(str, sizeof(str), format, localtime(&pcard->tLast));
	printf("卡号\t状态\t余额\t累计使用\t使用次数\t上次使用时间\n");
	printf("%s\t%d\t%.1f\t%.1f\t\t%d\t\t%s\n", pcard->aName, pcard->nStatus, pcard->fBalance, pcard->fTotalUse, pcard->nUseCount, str);
}
void disp_list(pList_card head)//遍历输出链表信息
{
	pList_card p = head;
	while (p->next != NULL)
	{
		p = p->next;
		message2_card(&(p->card));
	}
}
void release_cardList(pList_card head)//释放链表
{
	pList_card p = NULL, q = NULL;
	p = head;
	while (p->next != NULL)
	{
		q = p->next;
		p->next = q->next;
		free(q);
	}
	free(head);
}
//注销卡
int do_annul()//注销卡操作
{
	char card_name[50], card_pwd[20], * pstr1, * pstr2;
	printf("请输入卡号（长度1~18）：");
	scanf("%s", card_name);
	pstr1 = card_name;
	printf("请输入密码（长度1~8）：");
	scanf("%s", card_pwd);
	pstr2 = card_pwd;
	Card goal_card, * pcard = NULL;
	pcard = validata(pstr1, pstr2);//验证卡号与密码
	if (pcard == NULL)
		return 0;
	if (pcard->nStatus == 1)//正在上机的卡无法注销
	{
		printf("该卡正在上机！");
		return 0;
	}
	goal_card = *pcard;
	float money = 0;
	money = goal_card.fBalance;
	int sign = money_status(pstr1, money, 1);//将销卡金额存入消费记录文件
	if (sign == 0)
	{
		printf("消费记录信息更新失败！");
		return 0;
	}
	else
	{
		goal_card.fTotalUse -= goal_card.fBalance;//累计金额
		goal_card.fBalance = 0;//余额
		goal_card.nUseCount++;//使用次数
		goal_card.tLast = time(NULL);//最后使用时间
		goal_card.nDel = 1;//删除状态
	}
	pcard = &goal_card;
	char* pathcard = NULL;
	char path[100];
	strcpy(path, path_card(pcard->aName));//单独文件路径
	pathcard = path;
	int num = save_card(pcard, pathcard, "a");//添加注销卡信息至卡的单独文件
	if (num == 0)
		printf("更新信息失败！");
	pList_card head = NULL;
	head = update_file(&goal_card);//更新所有卡所在文件中该卡的信息
	if (head == NULL)
	{
		printf("文件更新失败！");
	}
	else
		release_cardList(head);
	message3_card(&goal_card, money);
	return 1;
}
void message3_card(const Card* pcard, const float money)//注销卡后显示卡信息
{
	char str[50], * format = "%Y-%m-%d %H:%M:%S";
	strftime(str, sizeof(str), format, localtime(&pcard->tLast));
	printf("卡号\t退费\t余额\t累计金额\t使用时间\n");
	printf("%s\t%.1f\t%.1f\t%.1f\t\t%s\n", pcard->aName, money, pcard->fBalance, pcard->fTotalUse, str);
}
//上机
Card* do_logon(const char* pName, const char* pPwd)//进行上机验证
{
	Card* pcard = NULL;
	Card goal_card;
	pcard = queryCard(pName);
	if (pcard == NULL)
	{
		printf("卡号密码错误！");
		return NULL;
	}
	if (strcmp(pcard->aPwd, pPwd) != 0)
	{
		printf("卡号密码错误！");
		return NULL;
	}
	if (pcard->nDel == 1)
	{
		printf("该卡已被注销！");
		return NULL;
	}
	goal_card = *pcard;
	//goal_card.nStatus = 1;//表示上机
	goal_card.nUseCount++;//使用次数+1
	time_t time_now = time(NULL);
	goal_card.tLast = time_now;//更新上次使用时间为上机时间
	return &goal_card;
}
void message4_card(const Card* pcard)//上机后显示卡信息
{
	char str[50], * format = "%Y-%m-%d %H:%M:%S";
	strftime(str, sizeof(str), format, localtime(&pcard->tLast));
	printf("卡号\t余额\t上机时间\n");
	printf("%s\t%.1f\t%s\n", pcard->aName, pcard->fBalance, str);
}
Rule* bill_message()//消费类型选择
{
	Rule rule;
	Allrule allrule, * pallrule = NULL;
	pallrule = &allrule;
	FILE* fp = NULL;
	fp = fopen(ALLBILL_PATH, "r");
	if (fp == NULL)
	{
		printf("文件打开失败！");
		return NULL;
	}
	if (fread(pallrule, sizeof(Allrule), 1, fp) == 0)
	{
		printf("计费标准读取失败！");
		return NULL;
	}
	fclose(fp);
	rule.unit = allrule.Unit;//最小计费单元
	rule.charge = allrule.Charge;//每个计费单元费用
	rule.day_charge = allrule.Day_charge;//包天费用
	rule.night_charge = allrule.Night_charge;//包夜费用
	rule.amount = 0;
	int rate_type = -1;
	printf("请选择消费类别（0-普通；1-包夜；2-包天）：");
	do
	{
		scanf("%d", &rate_type);
		if (rate_type != 0 && rate_type != 1 && rate_type != 2)
			printf("输入错误！\n请重新输入：");
	} while (rate_type != 0 && rate_type != 1 && rate_type != 2);
	rule.ratetype = rate_type;//消费类别
	rule.starttime = time(NULL);//消费开始时间
	rule.endtime = 0;//消费结束时间0
	rule.del = 0;//未删除-0
	return &rule;
}
char* path_billdata(const char* pname)//消费记录信息路径名
{
	char* path_bill = NULL;
	char str1[100] = "D:\\AMS\\AccountManagement\\billing_file\\", * str2 = "_fill.txt";
	strcat(str1, pname);
	strcat(str1, str2);
	path_bill = str1;
	return path_bill;
}
int bill_addto_file(const Rule* rule, const Card card)//将消费类型信息存入文件
{
	char path[100];
	strcpy(path, path_billdata(card.aName));
	int sign = save_bill(rule, path, "w");
	if (sign == 0)
		return 0;
	else return 1;
}
//下机
Card* do_settle(const char* pName, const char* pPwd,float *pmoney)//进行下机操作，pmoney用于返回消费金额
{
	Card* pcard = NULL;
	Card goal_card;
	time_t now_time = time(NULL);
	double diff_time = 0;
	pcard = queryCard(pName);
	if (pcard == NULL)
	{
		printf("卡号密码错误！");
		return NULL;
	}
	if (strcmp(pcard->aPwd, pPwd) != 0)
	{
		printf("卡号密码错误！");
		return NULL;
	}
	if (pcard->nDel == 1)
	{
		printf("该卡已被注销！");
		return NULL;
	}
	goal_card = *pcard;
	char* ppath;
	ppath = path_billdata(goal_card.aName);
	char bill_path[100];
	strcpy(bill_path, ppath);
	Rule *pbill=(Rule*)malloc(sizeof(Rule));
	FILE* fp = NULL;
	fp = fopen(bill_path, "r");
	if (fp == NULL)
	{
		printf("计费信息文件打开失败！");
		return NULL;
	}
	if (fread(pbill, sizeof(Rule), 1, fp) == 0)
	{
		printf("计费信息读取失败！");
		return NULL;
	}
	Rule bill_rule = *pbill;
	bill_rule.endtime = now_time;
	if (bill_rule.ratetype == 0)
	{
		diff_time = difftime(bill_rule.endtime, bill_rule.starttime);
		bill_rule.amount = ((diff_time / 60) / bill_rule.unit) * bill_rule.charge;
	}
	else if (bill_rule.ratetype == 1)
	{
		bill_rule.amount = bill_rule.night_charge;
	}
	else
		bill_rule.amount = bill_rule.day_charge;
	*pmoney = bill_rule.amount;//消费金额
	if (bill_rule.amount > goal_card.fBalance)//判断卡余额是否足够
	{
		printf("卡中余额不足！");
		return NULL;
	}
	else
	{
		goal_card.fBalance -= bill_rule.amount;//卡中余额更新
		goal_card.nStatus = 0;//更新卡状态：0-未上机
		goal_card.nUseCount++;//使用次数加1
		goal_card.tLast = now_time;//最后使用时间更新
		bill_rule.del = 1;//删除标志：1-已删除
	}
	int sign = money_status(goal_card.aName, bill_rule.amount, 2);//将消费金额存入消费记录文件
	if (sign == 0)
	{
		printf("消费记录更新失败！");
		return NULL;
	}
	int sign_turnover = putin_turnover(bill_rule.amount);
	if (sign_turnover == 0)
	{
		printf("添加至营业额文件失败！");
	}
	if (save_bill(&bill_rule, bill_path, "w") == 0)
	{
		printf("文件中计费信息更新失败！");
		return NULL;
	}
	return &goal_card;
}
void message5_card(const Card* pcard,const float money)//下机后显示卡信息
{
	char str[50], * format = "%Y-%m-%d %H:%M:%S";
	strftime(str, sizeof(str), format, localtime(&pcard->tLast));
	printf("卡号\t消费\t余额\t下机时间\n");
	printf("%s\t%.1f\t%.1f\t%s\n", pcard->aName,money, pcard->fBalance, str);
}
//充值
Card* validata(const char* pname, const char* ppwd)//验证卡号密码
{
	Card* pcard = NULL;
	Card goal_card;
	pcard = queryCard(pname);
	if (pcard == NULL)
		return NULL;
	if (strcmp(pcard->aPwd, ppwd) != 0)
		return NULL;
	goal_card = *pcard;
	return &goal_card;
}
int do_addmoney()//充值的一系列操作
{
	char card_name[50], card_pwd[20], * pstr1, * pstr2;
	printf("请输入卡号（长度1~18）：");
	scanf("%s", card_name);
	pstr1 = card_name;
	printf("请输入密码（长度1~8）：");
	//scanf("%s", card_pwd);
	getchar();//接收回车键
	pstr2 = protect_pwd();//密码保护
	strcpy(card_pwd, pstr2);
	pstr2 = card_pwd;
	Card goal_card, * pcard = NULL;
	pcard = validata(pstr1, pstr2);
	if (pcard == NULL)
		return 0;
	if (pcard->nDel == 1)
	{
		printf("该卡已被注销！");
		return 0;
	}
	goal_card = *pcard;
	float money = 0;
	printf("请输入充值金额：");
	scanf("%f", &money);
	int sign = money_status(pstr1, money, 0);//将充值金额存入消费记录文件
	if (sign == 0)
	{
		printf("消费记录信息更新失败！");
		return 0;
	}
	else
	{
		goal_card.fBalance += money;//余额
		goal_card.fTotalUse += money;//累计金额
		goal_card.nUseCount++;//使用次数
		goal_card.tLast = time(NULL);//最后使用时间
	}
	pcard = &goal_card;
	char* pathcard = NULL;
	char path[100];
	strcpy(path, path_card(pcard->aName));//单独文件路径
	pathcard = path;
	int num = save_card(pcard, pathcard, "a");//添加充值信息至卡的单独文件
	if (num == 0)
		printf("更新信息失败！");
	pList_card head = NULL;
	head = update_file(&goal_card);//更新所有卡所在文件中该卡的信息
	if (head == NULL)
	{
		printf("文件更新失败！");
	}
	else
		release_cardList(head);
	message6_card(&goal_card, money);
	return 1;
}
void message6_card(const Card* pcard, const float money)//充值后显示卡信息
{
	char str[50], * format = "%Y-%m-%d %H:%M:%S";
	strftime(str, sizeof(str), format, localtime(&pcard->tLast));
	printf("卡号\t充值\t余额\t充值时间\n");
	printf("%s\t%.1f\t%.1f\t%s\n", pcard->aName, money, pcard->fBalance, str);
}
//退费
int do_refundmoney()//退费的一系列操作
{
	char card_name[50], card_pwd[20], * pstr1, * pstr2;
	printf("请输入卡号（长度1~18）：");
	scanf("%s", card_name);
	pstr1 = card_name;
	printf("请输入密码（长度1~8）：");
	//scanf("%s", card_pwd);
	getchar();//接收回车键
	pstr2 = protect_pwd();//密码保护
	strcpy(card_pwd, pstr2);
	pstr2 = card_pwd;
	Card goal_card, * pcard = NULL;
	pcard = validata(pstr1, pstr2);
	if (pcard == NULL)
		return 0;
	if (pcard->nDel == 1)
	{
		printf("该卡已被注销！");
		return 0;
	}
	goal_card = *pcard;
	float money = 0;
	printf("请输入退费金额：");
	scanf("%f", &money);
	if (money > goal_card.fBalance)
	{
		printf("退费金额超出余额！");
		return 0;
	}
	int sign = money_status(pstr1, money, 1);//将退费金额存入消费记录文件
	if (sign == 0)
	{
		printf("消费记录更新失败！");
		return 0;
	}
	else
	{
		goal_card.fBalance -= money;//余额
		goal_card.fTotalUse -= money;//累计金额
		goal_card.nUseCount++;//使用次数
		goal_card.tLast = time(NULL);//最后使用时间
	}
	pcard = &goal_card;
	char* pathcard = NULL;
	char path[100];
	strcpy(path, path_card(pcard->aName));//单独文件路径
	pathcard = path;
	int num = save_card(pcard, pathcard, "a");//添加退费信息至卡的单独文件
	if (num == 0)
		printf("更新信息失败！");
	pList_card head = NULL;
	head = update_file(&goal_card);//更新所有卡所在文件中该卡的信息
	if (head == NULL)
	{
		printf("文件更新失败！");
	}
	else
		release_cardList(head);
	message7_card(&goal_card, money);
	return 1;
}
void message7_card(const Card* pcard, const float money)//退费后显示卡信息
{
	char str[50], * format = "%Y-%m-%d %H:%M:%S";
	strftime(str, sizeof(str), format, localtime(&pcard->tLast));
	printf("卡号\t退费\t余额\t退费时间\n");
	printf("%s\t%.1f\t%.1f\t%s\n", pcard->aName, money, pcard->fBalance, str);
}
//消费记录
char* bill_manage_path(const char* pname)//消费记录存入文件路径
{
	char* bill_manage_path = NULL;
	char str1[100] = "D:\\AMS\\AccountManagement\\billing_file\\bill_manage\\", * str2 = "_fee.txt";
	strcat(str1, pname);
	strcat(str1, str2);
	//bill_manage_path = str1;
	return str1;
}
int save_money_status(const Manage* manage, const char* money_path, const char* mode)//保存费用信息至文件
{
	FILE* fp = NULL;
	char path[100];
	strcpy(path, money_path);
	fp = fopen(path, mode);
	if (fp == NULL)
	{
		printf("文件打开失败！");
		return 0;
	}
	size_t size = fwrite(manage, sizeof(Manage), 1, fp);
	fclose(fp);
	if (size == 0)
	{
		printf("信息写入失败！");
		return 0;
	}
	else return 1;
}
int money_status(const char* pname, const float money, const int operate)//完善费用状态信息
{
	Manage manage;
	strcpy(manage.cardName, pname);//卡名
	manage.operation = operate;//操作类别
	manage.money = money;//金额
	manage.del = 0;
	manage.operationtime = time(NULL);
	char* ppath = NULL, money_path[100];
	ppath = bill_manage_path(pname);
	strcpy(money_path, ppath);
	int sign = save_money_status(&manage, money_path, "a");//保存消费信息至文件
	if (sign == 0)
		return 0;
	else
		return 1;
}
pManage_list make_managelist()//制作消费记录空链表
{
	pManage_list head = NULL;
	pManage_list tail = NULL;
	head = (pManage_list)malloc(sizeof(Manage_list));
	if (head == NULL)
		return NULL;//头结点申请内存失败,返回NULL
	head->next = NULL;
	tail = head;
	return head;
}
pManage_list add_managelist(pManage_list head, Manage add_manage)//在消费记录链表尾添加结点
{
	pManage_list p1 = head, add = NULL;
	add = (pManage_list)malloc(sizeof(Manage_list));
	add->manage = add_manage;
	add->next = NULL;
	while (p1->next != NULL)
	{
		p1 = p1->next;
	}
	p1->next = add;
	return head;
}
void look_manage(Manage* manage)//展示链表结点中的一条消费记录
{
	char str[50], * format = "%Y-%m-%d %H:%M:%S";
	strftime(str, sizeof(str), format, localtime(&manage->operationtime));
	if (manage->operation == 0)
	{
		printf("充值\t时间\n");
		printf("%.1f\t%s\n", manage->money, str);
	}
	else if (manage->operation == 1)
	{
		printf("退费\t时间\n");
		printf("%.1f\t%s\n", manage->money, str);
	}
	else
	{
		printf("消费\t时间\n");
		printf("%.1f\t%s\n", manage->money, str);
	}
}
void disp_manage(pManage_list head)//遍历消费记录链表
{
	pManage_list p = head;
	while (p->next != NULL)
	{
		p = p->next;
		look_manage(&(p->manage));
	}
}
void release_managelist(pManage_list head)//释放链表
{
	pManage_list p = NULL, q = NULL;
	p = head;
	while (p->next != NULL)
	{
		q = p->next;
		p->next = q->next;
		free(q);
	}
	free(head);
}
int do_billrecord()//进行消费记录查询操作
{
	char card_name[50], card_pwd[20], * pstr1, * pstr2;
	printf("请输入卡号（长度1~18）：");
	scanf("%s", card_name);
	pstr1 = card_name;
	printf("请输入密码（长度1~8）：");
	//scanf("%s", card_pwd);
	getchar();//接收回车键
	pstr2 = protect_pwd();//密码保护
	strcpy(card_pwd, pstr2);
	pstr2 = card_pwd;
	Card goal_card, * pcard = NULL;
	pcard = validata(pstr1, pstr2);
	if (pcard == NULL)
		return 0;
	goal_card = *pcard;
	char* ppath = NULL, fee_path[100];
	ppath = bill_manage_path(goal_card.aName);//消费记录文件的路径
	strcpy(fee_path, ppath);
	Manage tool_manage;
	pManage_list head = make_managelist();
	FILE* fp;
	fp = fopen(fee_path, "r");
	if (fp == NULL)
	{
		printf("文件打开失败！");
		return 0;
	}
	while (1)
	{
		if (fread(&tool_manage, sizeof(Manage), 1, fp) == 0)//读取文件信息至结构体
		{
			break;
		}
		head = add_managelist(head, tool_manage);//将结构体信息存入链表
	}
	fclose(fp);//关闭文件
	disp_manage(head);//遍历链表信息
	release_managelist(head);//释放链表
	return 1;
}
//密码加密
char* protect_pwd()//密码保护
{
	char cardpwd[20] = { '\0' };
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
```
+ card_file.c文件
```c
#pragma warning(disable:4996)
#define _CRT_SECURE_NO_WARNINGS
#pragma once
#include<stdio.h>
#include<stdlib.h>
#include<time.h>
#include<string.h>
#include"service.h"
#define PATH "D:\\AMS\\AccountManagement\\data\\card_data.txt"//卡信息路径
#define ALLBILL_PATH "D:\\AMS\\AccountManagement\\billing_file\\bill_message\\allbill_rule.txt"//计费标准信息保存路径
#define NUM 100
//添加卡相关函数
int save_card(const Card* p_card, const char* p_path, const char* mode)//将卡的信息保存到文件中
{
	FILE* fp = NULL;
	fp = fopen(p_path, mode);
	if (fp == NULL)
		return 0;
	size_t size=fwrite(p_card, sizeof(Card), 1, fp);
	fclose(fp);
	if (size == 0)
		return 0;
	return 1;
}
//查询卡相关函数
int queryCard1(const char* pName)//使用结构体精确查询
{
	extern Card aCard[NUM];
	FILE* fp = NULL;
	fp = fopen(PATH, "rb");
	if (fp == NULL)
	{
		printf("文件打开失败！");
		exit(0);
	}
	int searchnum = -1;
	for (int i = 0; i < NUM; i++)
	{
		if (fread(&aCard[i], sizeof(Card), 1, fp) == 0)
		{
			//printf("文件读取失败！\n");
			break;
		}
		if (strcmp(pName, &(aCard[i].aName)) == 0)
		{
			searchnum = i;
			//break;
		}
	}
	fclose(fp);
	return searchnum;
}
Card* queryCard(const char* pName)//使用链表查找信息（精确查找）
{
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
	p = search_card(head, pName);//寻找目标结点
	if (p == NULL)
		return NULL;
	goal_card = p->card;
	release_cardList(head);//释放链表
	return &goal_card;
}
pList_card* queryCards(const char* pName, int* pIndex)//使用链表模糊查找卡信息
{
	FILE* fp;
	fp = fopen(PATH, "rb");//打开文件
	if (fp == NULL)
	{
		printf("文件打开失败！");
		exit(0);
	}
	pList_card head = NULL,goal_head=NULL;
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
	goal_head = search_cards(head, pName, pIndex);//将查询信息存入目标链表
	release_cardList(head);//释放链表
	return goal_head;//返回目标链表头指针
}
//上机相关函数
int insert_newfile(const pList_card head, const char* p_path)//将新链表信息写入文件
{
	pList_card p = head->next;
	Card tool_card;
	tool_card = p->card;
	int sign = save_card(&tool_card, PATH, "w");//清除文件中原来内容重新写入第一个结点信息
	if (sign == 0)
	{
		//printf("重新写入信息失败！");
		return 0;
	}
	while (p->next != NULL)
	{
		p = p->next;
		tool_card = p->card;
		sign = save_card(&tool_card, PATH, "a");//以追加形式将后面结点写入文件
		if (sign == 0)
		{
			//printf("重新写入信息失败！");
			return 0;
		}
	}
	return 1;//写入成功返回1，否则返回0
}
pList_card update_file(const Card* pcard)//将原文件信息存入链表，对链表更新信息，再重新写入文件
{
	FILE* fp = NULL;
	fp = fopen(PATH, "rb");//打开文件
	if (fp == NULL)
	{
		//printf("文件打开失败！");
		return NULL;
	}
	pList_card head = NULL, p = NULL;
	head = make();
	Card tool_card;
	while (1)
	{
		if (fread(&tool_card, sizeof(Card), 1, fp) == 0)//读取文件信息至结构体
		{
			break;
		}
		head = add_message(head, tool_card);//将结构体信息存入链表
	}
	fclose(fp);//关闭文件
	p = search_card(head, pcard->aName);//寻找目标结点
	p->card = (*pcard);//修改结点信息
	int sign = insert_newfile(head, PATH);
	if (sign == 0)
	{
		//printf("文件更新失败！");
		return NULL;
	}
	return head;//返回链表头结点，失败返回NULL
}
//下机相关函数
int save_bill(const Rule* p_bill, const char* p_path, const char* mode)//将计费的信息保存到文件中
{
	FILE* fp = NULL;
	fp = fopen(p_path, mode);
	if (fp == NULL)
		return 0;
	size_t size = fwrite(p_bill, sizeof(Rule), 1, fp);
	fclose(fp);
	if (size == 0)
		return 0;
	return 1;
}
```
+ manage.c文件
```c
#pragma warning(disable:4996)
#define _CRT_SECURE_NO_WARNINGS
#pragma once
#include<stdio.h>
#include<stdlib.h>
#include<time.h>
#include<string.h>
#include"service.h"
#define ALLBILL_PATH "D:\\AMS\\AccountManagement\\billing_file\\bill_message\\allbill_rule.txt"//计费标准信息保存路径
#define MANAGER_PATH "D:\\AMS\\AccountManagement\\data\\manager_data.txt"//管理员信息保存路径
#define TURNOVER_PATH "D:\\AMS\\AccountManagement\\billing_file\\bill_message\\turnover.txt"//营业总额文件路径
//#define MANAGE_PATH "D:\\AMS\\AccountManagement\\data\\manage_data.txt"
int make_allrule()//添加新标准至文件
{
	Allrule totalrule;
	printf("请输入最小计费单元(分钟)：");
	scanf("%d", &totalrule.Unit);
	printf("请输入每单元时间的费用：");
	scanf("%f", &totalrule.Charge);
	printf("请输入包天费用：");
	scanf("%f", &totalrule.Day_charge);
	printf("请输入包夜费用：");
	scanf("%f", &totalrule.Night_charge);
	FILE* fp = NULL;
	fp = fopen(ALLBILL_PATH, "w");//打开文件，只读（文本）
	if (fp == NULL)
		return 0;
	size_t size = fwrite(&totalrule, sizeof(Allrule), 1, fp);
	if (size == 0)
	{
		printf("计费标准写入文件失败！");
		return 0;
	}
	fclose(fp);
	display_allrule();
	return 1;
}
void display_allrule()//显示计费标准信息
{
	Allrule totalrule;
	FILE* fp = NULL;
	fp = fopen(ALLBILL_PATH, "r");
	if (fp == NULL)
	{
		printf("文件打开失败！");
	}
	if (fread(&totalrule, sizeof(Allrule), 1, fp) == 0)
		printf("文件读取失败！");
	fclose(fp);
	printf("---计费标准信息如下---\n");
	printf("计费单元\t单元费用\t包天费用\t包夜费用\n");
	printf("%d\t\t%.2f\t\t%.2f\t\t%.2f\n", totalrule.Unit, totalrule.Charge, totalrule.Day_charge, totalrule.Night_charge);
}
int add_manager()//添加新管理员
{
	Manager manager;
	printf("请输入管理员名：");
	scanf("%s", manager.name);
	printf("请输入密码：");
	scanf("%s", manager.pwd);
	manager.privilge = 1;
	manager.del = 0;
	FILE* fp = NULL;
	fp = fopen(MANAGER_PATH, "ab");
	if(fp==NULL)
	{
		printf("文件打开失败！");
		return 0;
	}
	size_t size = fwrite(&manager, sizeof(Manager), 1, fp);
	fclose(fp);
	if (size == 0)
	{
		printf("管理员添加失败！");
		return 0;
	}
	else
	{
		printf("管理员添加成功！");
		return 1;
	}
}
pList_manager make_manager()//制作一个空链表(管理员)
{
	pList_manager head = NULL;
	pList_manager tail = NULL;
	head = (pList_manager)malloc(sizeof(pList_manager));
	if (head == NULL)
		return NULL;//头结点申请内存失败,返回NULL
	head->next = NULL;
	tail = head;
	return head;
}
pList_manager add_manager_message(pList_manager head, Manager message)//传入链表头指针，manager中信息（值传递）
{
	pList_manager p1 = head, add = NULL;
	add = (pList_manager)malloc(sizeof(List_manager));
	add->manager = message;
	add->next = NULL;
	while (p1->next != NULL)
	{
		p1 = p1->next;
	}
	p1->next = add;
	return head;
}
pList_manager search_manager(pList_manager head, const char* pName)//寻找目标结点，返回结点指针，找不到返回NULL
{
	pList_manager p = head;
	int sign = 0;
	while (p->next != NULL)//遍历链表
	{
		p = p->next;
		if (strcmp(&p->manager.name, pName) == 0)
		{
			sign = 1;
			break;
		}
	}
	if (sign == 0)
		return NULL;
	else return p;
}
void release_managerList(pList_manager head)//释放管理员链表
{
	pList_manager p = NULL, q = NULL;
	p = head;
	while (p->next != NULL)
	{
		q = p->next;
		p->next = q->next;
		free(q);
	}
	free(head);
}
Manager* queryManager(const char* pName)//使用链表精确查找管理员信息
{
	FILE* fp;
	fp = fopen(MANAGER_PATH, "rb");//打开文件，只读（二进制）
	if (fp == NULL)
	{
		printf("文件打开失败！");
		return NULL;
	}
	pList_manager head = NULL, p = NULL;
	head = make_manager();//制作空链表
	Manager tool_manager, goal_manager;
	while (1)
	{
		if (fread(&tool_manager, sizeof(Manager), 1, fp) == 0)//读取文件信息至结构体
		{
			break;
		}
		head = add_manager_message(head, tool_manager);//将结构体信息存入链表
	}
	fclose(fp);//关闭文件
	p = search_manager(head, pName);//寻找目标结点
	if (p == NULL)
		return NULL;
	goal_manager = p->manager;
	release_managerList(head);//释放链表
	return &goal_manager;
}
int do_manage(const char* pname, const char* ppwd)//管理员验证并修改计费标准
{
	Manager manager,*p;
	p = queryManager(pname);
	if (p == NULL)
		return 0;
	if (strcmp(&p->pwd, ppwd) != 0)
		return 0;
	manager = *p;
	int sign=make_allrule();
	if (sign == 1)
		printf("计费标准修改成功！");
	else
		printf("计费标准修改失败！");
	return 1;
}
//营业额相关函数
pTurnoverlist make_turnoverlist()//制作营业额空链表
{
	pTurnoverlist head = NULL;
	pTurnoverlist tail = NULL;
	head = (pTurnoverlist)malloc(sizeof(Turnoverlist));
	if (head == NULL)
		return NULL;//头结点申请内存失败,返回NULL
	head->next = NULL;
	tail = head;
	return head;
}
pTurnoverlist add_turnover(pTurnoverlist head, Turnover add_turnover)//在链表尾新增结点信息
{
	pTurnoverlist p1 = head, add = NULL;
	add = (pTurnoverlist)malloc(sizeof(Turnoverlist));
	add->turnover = add_turnover;
	add->next = NULL;
	while (p1->next != NULL)
	{
		p1 = p1->next;
	}
	p1->next = add;
	return head;
}
void release_turnoverlist(pTurnoverlist head)//释放链表
{
	pTurnoverlist p = NULL, q = NULL;
	p = head;
	while (p->next != NULL)
	{
		q = p->next;
		p->next = q->next;
		free(q);
	}
	free(head);
}
pTurnoverlist file_putin_turnoverlist()//将文件中所有信息存入链表
{
	FILE* fp = NULL;
	fp = fopen(TURNOVER_PATH, "r");//只读
	if (fp == NULL)
	{
		printf("文件打开失败！");
		return 0;
	}
	pTurnoverlist head = make_turnoverlist();//制作空链表
	Turnover tool_turnover;
	while (1)
	{
		if (fread(&tool_turnover, sizeof(Turnover), 1, fp) == 0)//读取文件信息至结构体
		{
			break;
		}
		head = add_turnover(head, tool_turnover);//将结构体信息存入链表
	}
	fclose(fp);//关闭文件
	return head;
}
int putin_turnover(const float money)//将新的营业额写入文件中
{
	Turnover turnover;
	turnover.money = money;
	turnover.time = time(NULL);
	FILE* fp = NULL;
	fp = fopen(TURNOVER_PATH, "a");//尾部添加信息
	size_t size = fwrite(&turnover, sizeof(Turnover), 1, fp);
	fclose(fp);
	if (size == 0)
	{
		printf("营业额写入文件失败！");
		return 0;
	}
	else
		return 1;
}
int view_turnover(const char* pname, const char* ppwd)//查看营业总额
{
	Manager manager, * p;
	p = queryManager(pname);
	if (p == NULL)
		return 0;
	if (strcmp(&p->pwd, ppwd) != 0)
		return 0;
	manager = *p;
	float allmoney = 0;
	time_t nowtime = time(NULL);
	char str[50], * format = "%Y-%m-%d %H:%M:%S";
	strftime(str, sizeof(str), format, localtime(&nowtime));
	pTurnoverlist head = file_putin_turnoverlist();
	pTurnoverlist tool = head;
	while (tool->next != NULL)
	{
		tool = tool->next;
		allmoney += tool->turnover.money;
	}
	release_turnoverlist(head);
	printf("营业总额\t查看时间\n");
	printf("%.1f\t\t%s\n", allmoney, str);
	return 1;
}
```
+ menu.h文件
```c
#ifndef MENU_H
#define MENU_H

void outputMenu();  //声明输出菜单函数
void output_selectnum(int);  //声明输出所选菜单项函数
void add();  //声明添加卡函数
void query();  //声明查询卡函数
void annul();  //声明注销卡函数
void logon();  //声明上机函数
void settle();  //声明下机函数
void addMoney();  //声明充值函数
void refundMoney();  //声明退费函数
void billRecord();  //声明消费记录查询函数
//void exitApp();  //声明退出应用程序函数
void manage();   //声明管理函数
#endif
```
+ service.h文件
```c
#ifndef SERVICE
//卡结构体
typedef struct Card
{
	char aName[18];  //卡号，不能为空，长度为1~18个字符
	char aPwd[8];  //密码，不能为空，长度为1~8个字符
	int nStatus;  //卡状态：0-未上机；1-正在上机；2-已注销；3-失效
	time_t tStart;  //开卡时间
	time_t tEnd;  //截止时间
	float fTotalUse;  //累计金额
	time_t tLast;  //最后使用时间
	int nUseCount;  //使用次数
	float fBalance;  //余额
	int nDel;  //删除标志：0-未删除；1-已删除
}Card;
//计费标准信息
typedef struct bill_rule
{
	time_t starttime;  //开始时间
	time_t endtime;  //结束时间
	float amount;  //消费金额
	int unit;  //最小计费单元（分钟）
	float charge;  //每个计费单元的收费
	float night_charge;  //包夜费用
	float day_charge;  //包天费用
	int ratetype;  //收费类别：0-普通；1-包夜；2-包天
	int del;  //删除标志：0-未删除；1-已删除
}Rule;
//整体标准
typedef struct all_rule
{
	int Unit;//最小计费单元
	float Charge;//每个计费单元收费
	float Day_charge;//包天费用
	float Night_charge;//包夜费用
}Allrule;
//充值退费信息
typedef struct bill_manage
{
	char cardName[18];  //卡号
	time_t operationtime;  //操作时间
	int operation;  //操作类别：0-充值；1-退费;2-下机
	float money;  //费用
	int del;  //删除标志：0-未删除；1-已删除
}Manage;
//管理员信息
typedef struct manager
{
	char name[18];  //用户名
	char pwd[8];  //密码
	int privilge;  //权限等级
	int del;  ////删除标志：0-未删除；1-已删除
}Manager;
//管理员链表结点
typedef struct List_manager
{
	Manager manager;
	struct List_manager* next;
}List_manager,*pList_manager;
//卡链表结点
typedef struct List_card   
{
	Card card;
	struct List_card* next;
}List_card,*pList_card;
//消费记录结点
typedef struct managelist
{
	Manage manage;
	struct managelist* next;
}Manage_list, * pManage_list;
//营业额结构体
typedef struct turnover
{
	float money;//营业收入
	time_t time;//收入时间
}Turnover;
//营业额结点
typedef struct turnover_list
{
	Turnover turnover;
	struct turnover_list* next;
}Turnoverlist, * pTurnoverlist;
//添加卡相关函数
void input_card(Card* card);//开卡添加信息
char* path_card(const char* pname);//单独文件路径名
int save_card(const Card* p_card, const char* p_path,const char* mode);//保存开卡信息至文件
void message1_card(const Card* p_card);//显示开卡信息
//查询卡相关函数
void message2_card(const Card* pcard);//显示查询卡信息
int queryCard1(const char* pName);//使用数组准确查找
pList_card make();//制作空链表
pList_card add_message(pList_card head, Card message_card);//传入链表头指针，card中信息（值传递）
void release_cardList(pList_card head);//释放链表
pList_card search_card(pList_card head, const char* pName);
Card* queryCard(const char* pName);//使用链表准确查找
void disp_list(pList_card head);//遍历输出链表信息
pList_card search_cards(pList_card head, const char* pName, int* pIndex);//模糊查找，返回新建链表头结点指针，找不到返回NULL
pList_card* queryCards(const char* pName, int* pIndex);//使用链表模糊查找卡信息
//注销卡
int do_annul();//注销卡操作
void message3_card(const Card* pcard, const float money);//注销卡后显示卡信息
//上机相关函数
Card* do_logon(const char* pName, const char* pPwd);//进行上机验证
void message4_card(const Card* pcard);//上机后显示卡信息
int insert_newfile(const pList_card head, const char* p_path);//将新链表信息写入文件
pList_card update_file(const Card* pcard);//将文件信息存入链表，对链表更新信息，再重新写入文件
Rule* bill_message();//消费类型选择
char* path_billdata(const char* pname);//消费记录信息路径名
int bill_addto_file(const Rule* rule, const Card card);//将消费类型信息存入文件
int save_bill(const void* p_bill, const char* p_path, const char* mode);//将计费的信息保存到文件中
//下机相关函数
Card* do_settle(const char* pName, const char* pPwd,float *pmoney);//进行下机操作，pmoney用于返回消费金额
void message5_card(const Card* pcard,const float money);//下机后显示卡信息
//充值相关函数
Card* validata(const char* pname, const char* ppwd);//验证卡号密码
int do_addmoney();//充值的一系列操作
void message6_card(const Card* pcard, const float money);//充值后显示卡信息
//退费相关函数
int do_refundmoney();//充值的一系列操作
void message7_card(const Card* pcard, const float money);//退费后显示卡信息
//消费记录相关函数
char* bill_manage_path(const char* pname);//消费记录存入文件路径
int save_money_status(const Manage* manage, const char* money_path, const char* mode);//保存费用信息至文件
int money_status(const char* pname, const float money, const int operate);//完善费用状态信息
pManage_list make_managelist();//制作消费记录空链表
pManage_list add_managelist(pManage_list head, Manage add_manage);//在消费记录链表尾添加结点
void look_manage(Manage* manage);//展示链表结点中的一条消费记录
void disp_manage(pManage_list head);//遍历消费记录链表
void release_managelist(pManage_list head);//释放链表
int do_billrecord();//进行消费记录查询操作
//营业额相关函数
pTurnoverlist make_turnoverlist();//制作营业额空链表
pTurnoverlist add_turnover(pTurnoverlist head, Turnover add_turnover);//在链表尾新增结点信息
void release_turnoverlist(pTurnoverlist head);//释放链表
pTurnoverlist file_putin_turnoverlist();//将文件中所有信息存入链表
int putin_turnover(const float money);//将新的营业额写入文件中
int view_turnover(const char* pname, const char* ppwd);//查看营业总额
//管理员相关函数
int add_manager();//添加新管理员
pList_manager make_manager();//制作一个空链表(管理员)
pList_manager add_manager_message(pList_manager head, Manager message);//传入链表头指针，manager中信息（值传递）
pList_manager search_manager(pList_manager head, const char* pName);//寻找目标结点，返回结点指针，找不到返回NULL
void release_managerList(pList_manager head);//释放管理员链表
Manager* queryManager(const char* pName);//使用链表精确查找管理员信息
int do_manage(const char* pname, const char* ppwd);//管理员验证并修改计费标准
int make_allrule();//添加新标准至文件
void display_allrule();//显示计费标准信息
//额外
char* protect_pwd();//密码保护
#define SERVICE
#endif
```
