# AMSʵ��˵���Լ�����
## ˵��
+ ���ڶ�д�ļ����ղ��ã����Խ�����Ϣ�����ļ�������Ϊ���룬����Ӱ��������У�
+ AMS���ļ��д����ҵĵ����ϵ�D�̣���д�ļ���·�������ض��ģ�ֻȷ�����ҵĵ������������У�
+ ��д����ʱ�Ҳ�δ��ȫ���յ������ϵ�Ҫ��ȥд��ֻ���Ķ����蹦�ܺ��Լ�ȥд���룻
+ д����ʱ�ҽ��󲿷ֺ���д��card_service.c�ļ��У�����д��menu.c��manage.c�ļ��У����еĺ��������Լ����нṹ�嶨��λ��service.h�ļ��У��������ļ���Щ�ң�
+ card_service.c�ļ��еĺ����ǽ��˵��еĸ����������躯������һ�𣻲�δ���ݵ����������нṹ���������Ҳ�ͬ��;���벻ͬ.c�ļ��У�
+ ����д����ʱ������һ����һ���������кõ��뷨ʱ������ǰ����д�������������Ż����������ڴ���֮��Ĺ����ԣ����ҽ�������Ķ������Դ����кܶ�ط��Ĳ��㣻
+ ѡ��˵�ʱ��Ҫ��ѡ����9���һ������Ա�����ƶ����ѹ���Ȼ�����ϻ����»�ʱ������ȷ�Ʒѣ�
+ �˵��еĹ���������8���˵�ѡ��ֱ�Ϊ����Ա������ʹ���߲��棬�ڲ˵��н����Ƿ���һ�𣬴˴����в��㣻
+ �����в�δ��Ӹ���ʱ�������ѯ���Ѽ�¼�Ĺ��ܣ�

## ����
+ main.c�ļ�
```c
#pragma warning(disable:4996)
#define _CRT_SECURE_NO_WARNINGS
#include<stdio.h>
#include<stdlib.h>
#include"menu.h"

int main()
{
	printf("��ӭ����Ʒѹ���ϵͳ��\n\n");
	char str[20];
	int select_num = -1;
	do
	{
		//������ɫ
		system("color 1f");
		//�˵�ҳ�����
		outputMenu(); 
		//����ѡ��˵����
		scanf("%s",str);
		select_num = atoi(str);
		//�����ѡ�˵���
		output_selectnum(select_num);
		
	} while (select_num != 10);
	return 0;
}
```
+ menu.c�ļ�
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
//����˵�
void outputMenu()
{
	//int select_num = -1;
	printf("-----�˵�-----\n");
	printf("1.��ӿ�\n2.��ѯ��\n3.ע����\n");
	printf("4.�ϻ�\n5.�»�\n");
	printf("6.��ֵ\n7.�˷�\n8.���Ѽ�¼��ѯ\n");
	printf("9.����\n10.�˳�\n");
	printf("��������ѡ�˵��������(1~10):");
}
//�����ѡ�˵����
void output_selectnum(int select_num)
{
	switch (select_num)
	{
	case 1:
		printf("-----��ӿ�-----\n");
		add();
		break;
	case 2:
		printf("-----��ѯ��-----\n");
		query();
		break;
	case 3:
		printf("-----ע����-----\n");
		annul();
		break;
	case 4:
		printf("-----�ϻ�-----\n");
		logon();
		break;
	case 5:
		printf("-----�»�-----\n");
		settle();
		break;
	case 6:
		printf("-----��ֵ-----\n");
		addMoney();
		break;
	case 7:
		printf("-----�˷�-----\n");
		refundMoney();
		break;
	case 8:
		printf("---���Ѽ�¼��ѯ---\n");
		billRecord();
		break;
	case 9:
		printf("-----����-----\n");
		manage();
		break;
	case 10:
		printf("�˳�\n");
		break;
	default:
		printf("����Ĳ˵���Ŵ���\n"); 
	}
	printf("\n");
}
//��ӿ�
void add()
{
	Card card;
	input_card(&card);
	int num1 = save_card(&card, PATH, "a");//���������ļ������ļ��������п���
	char *pathcard=NULL;
	char path[100];
	strcpy(path, path_card(card.aName));
	pathcard = path;
	int num2 = save_card(&card, pathcard, "a");//����ӵĿ��ٶ�������һ���ļ�
	int sign = money_status(card.aName, card.fBalance, 0);//�����������Ϣ�������Ѽ�¼�����ļ�
	if (sign == 0)
		printf("���������Ϣ�����ļ�ʧ�ܣ�\n");
	else
	{
		if (num1 == 0 || num2 == 0)
			printf("��ӿ�ʧ�ܣ�\n");
		else
			printf("��ӿ��ɹ���\n");
		message1_card(&card);
	}
	system("pause");
}
//��ѯ��
void query()
{
	extern Card aCard[NUM];
	char card_name[50],*pstr;
	printf("�������ѯ�Ŀ��ţ�����1~18����");
	scanf("%s", card_name);
	pstr = card_name;
	//ʹ�ýṹ�����
	/*int cardnum = queryCard1(pstr);
	if (cardnum==-1)
		printf("û�иÿ���Ϣ��");
	else
	message2_card(&aCard[cardnum]);*/
	//ʹ������׼ȷ����
	/*Card target_card;
	target_card = *queryCard(pstr);
	if(queryCard(pstr) ==NULL)
		printf("û�иÿ���Ϣ��");
	else
		message2_card(&target_card);*/
	//ʹ������ģ������
	int num = 0;
	pList_card goal_head = queryCards(pstr, &num);
	if (goal_head->next == NULL)
		printf("û�иÿ���Ϣ��\n");
	else
		disp_list(goal_head);
	release_cardList(goal_head);
	system("pause");
}
//ע����
void annul()
{
	int sign = do_annul();
	if (sign == 0)
		printf("ע����ʧ�ܣ�\n");
	system("pause");
}
//�ϻ�
void logon()
{
	char card_name[50],card_pwd[20], *pstr1=NULL,*pstr2=NULL;
	printf("�������ϻ����ţ�����1~18����");
	scanf("%s", card_name);
	pstr1 = card_name;
	printf("�������ϻ����루����1~8����");
	//scanf("%s", card_pwd);
	getchar();//���ջس���
	pstr2 = protect_pwd();//���뱣��
	strcpy(card_pwd, pstr2);
	pstr2 = card_pwd;
	printf("---�ϻ���Ϣ����---\n");
	Card goal_card, * pcard = NULL;
	pcard=do_logon(pstr1,pstr2);//�ϻ���֤
	if (pcard == NULL)
		printf("�ϻ�ʧ�ܣ�\n");
	else if (pcard->nStatus != 0)//״̬
		printf("�ϻ�ʧ�ܣ�\n");
	else if (pcard->fBalance <= 0)//���
		printf("�ϻ�ʧ�ܣ�\n");
	else
	{
		pcard->nStatus = 1;
		goal_card = *pcard;
		Rule *prule= bill_message();//��������ѡ��
		Rule bill_rule;
		bill_rule = *prule;
		int sign= bill_addto_file(&bill_rule, goal_card);//�Ʒ���Ϣ�������ļ�
		if (sign == 0)
			printf("�Ʒ���Ϣ����ʧ�ܣ�\n");
		else
		{
			char* pathcard = NULL;
			char path[100];
			strcpy(path, path_card(goal_card.aName));//�����ļ�·��
			pathcard = path;
			int num = save_card(&goal_card, pathcard, "a");//����ϻ���Ϣ�����ĵ����ļ�
			if (num == 0)
				printf("������Ϣʧ�ܣ�\n");

			pList_card head = update_file(&goal_card);//���ļ���Ϣ�������������������Ϣ��������д���ļ�
			if (head == NULL)
			{
				printf("�ļ�����ʧ�ܣ�\n");
			}
			else
				release_cardList(head);
			message4_card(&goal_card);//�ϻ���ʾ����Ϣ
		}
	}
	system("pause");
}
//�»�
void settle()
{
	char card_name[50], card_pwd[20], * pstr1, * pstr2;
	float money=0,bill_money=0;//���ڼ�¼���ѽ��
	printf("�������»����ţ�����1~18����");
	scanf("%s", card_name);
	pstr1 = card_name;
	printf("�������»����루����1~8����");
	//scanf("%s", card_pwd);
	getchar();//���ջس���
	pstr2 = protect_pwd();//���뱣��
	strcpy(card_pwd, pstr2);
	pstr2 = card_pwd;
	printf("---�»���Ϣ����---\n");
	Card *pcard = NULL;
	pcard = do_settle(pstr1, pstr2,&money);
	//bill_money = money;
	if (pcard == NULL)
		printf("�»�ʧ�ܣ�\n");
	else
	{
		char* pathcard = NULL;
		char path[100];
		Card goal_card = *pcard;//��������save_card������pcard���ݶ�ʧ�������룬������goal_card��������
		strcpy(path, path_card(pcard->aName));//�����ļ�·��
		pathcard = path;
		int num = save_card(pcard, pathcard, "a");//����»���Ϣ�����ĵ����ļ�
		if (num == 0)
			printf("������Ϣʧ�ܣ�\n");
		pList_card head = NULL;
		head = update_file(&goal_card);//�������п������ļ��иÿ�����Ϣ
		if (head == NULL)
		{
			printf("�ļ�����ʧ�ܣ�\n");
		}
		else
			release_cardList(head);

		message5_card(&goal_card,money);//��ʾ�»���Ϣ
	}
	system("pause");
}
//��ֵ
void addMoney()
{
	int sign = do_addmoney();
	if (sign == 0)
		printf("��ֵʧ�ܣ�\n");
	system("pause");
}
//�˷�
void refundMoney()
{
	int sign = do_refundmoney();
	if (sign == 0)
		printf("�˷�ʧ�ܣ�\n");
	system("pause");
}
//���Ѽ�¼
void billRecord()
{
	int sign = do_billrecord();
	if (sign == 0)
		printf("���Ѽ�¼��ѯʧ�ܣ�\n");
	system("pause");
}
//����
void manage()
{
	int num = -1;
	printf("1.��ӹ���Ա\n2.�޸ļƷѱ�׼\n3.�鿴Ӫҵ��\n��ѡ���ţ�");
	scanf("%d", &num);
	switch (num) 
	{
	case 1:
		add_manager();
		break;
	case 2:
	{
		char manager_name[50], manager_pwd[20], * pname, * ppwd;
		printf("���������Ա����");
		scanf("%s", manager_name);
		pname = manager_name;
		printf("���������룺");
		//scanf("%s", manager_pwd);
		getchar();//���ջس���
		ppwd = protect_pwd();//���뱣��
		strcpy(manager_pwd, ppwd);
		ppwd = manager_pwd;
		int sign = do_manage(pname, ppwd);
		if (sign == 0)
		{
			printf("����");
		}
		break;
	}
	case 3:
	{
		char manager_name[50], manager_pwd[20], * pname, * ppwd;
		printf("���������Ա����");
		scanf("%s", manager_name);
		pname = manager_name;
		printf("���������룺");
		//scanf("%s", manager_pwd);
		getchar();//���ջس���
		ppwd = protect_pwd();//���뱣��
		strcpy(manager_pwd, ppwd);
		ppwd = manager_pwd;
		int sign = view_turnover(pname, ppwd);//�鿴Ӫҵ�ܶ�
		if (sign == 0)
		{
			printf("�鿴ʧ�ܣ�");
		}
		break;
	}
	default:
		printf("�����Ŵ���");
	}
	system("pause");
}
```
+ card_service.c�ļ�
```c
#pragma warning(disable:4996)
#define _CRT_SECURE_NO_WARNINGS
#pragma once
#include<stdio.h>
#include<stdlib.h>
#include<string.h>
#include<time.h>
#include"service.h"
#define PATH "D:\\AMS\\AccountManagement\\data\\card_data.txt"//����Ϣ·��
#define ALLBILL_PATH "D:\\AMS\\AccountManagement\\billing_file\\bill_message\\allbill_rule.txt"//�Ʒѱ�׼��Ϣ����·��
#define TURNOVER_PATH "D:\\AMS\\AccountManagement\\billing_file\\bill_message\\turnover.txt"//Ӫҵ�ܶ��ļ�·��
#define NUM 100
extern Card aCard[NUM]={0};
//��ӿ�
void input_card(Card* card)//���뿪����Ϣ
{
	char aName1[50] = { 0 }, aPwd1[20] = { 0 };
	struct tm* tStart1, * tEnd1;
	int sign = 0;
	printf("�����뿨�ţ�����1~18����");//���뿨�Ų��ж�
	do
	{
		scanf("%s", aName1);
		if (strlen(aName1) > 18)
			printf("�������\n���������룺");
		else {
			strcpy(card->aName, aName1);
			sign = 1;
		}
	} while (sign == 0);
	sign = 0;
	printf("���������루����1~8����");//�������벢�ж�
	do
	{
		scanf("%s", aPwd1);
		if (strlen(aPwd1) > 8)
			printf("�������\n���������룺");
		else {
			strcpy(card->aPwd, aPwd1);
			sign = 1;
		}
	} while (sign == 0);
	printf("�����뿪����");
	scanf("%f", &card->fBalance);
	card->fTotalUse = card->fBalance;
	card->nStatus = card->nUseCount = card->nDel = 0;
	card->tStart = card->tEnd = card->tLast = time(NULL);//ʱ�䴦��
	tStart1 = tEnd1 = localtime(&card->tStart);
	tEnd1->tm_year = tStart1->tm_year + 1;
	card->tEnd = mktime(tEnd1);
}
char* path_card(const char* pname)//�����ļ����и�����Ϣ·����
{
	char* path_card = NULL;
	char str1[100] = "D:\\AMS\\AccountManagement\\data\\all_update_message\\", * str2 = ".txt";
	strcat(str1, pname);
	strcat(str1, str2);
	path_card = str1;
	return path_card;
}
void message1_card(const Card* p_card)//��ʾ���������Ϣ
{
	printf("---��ӿ���Ϣ����---\n");
	printf("����\t����\t״̬\t�������\n");
	printf("%s\t%s\t%d\t%.2f\n", p_card->aName, p_card->aPwd, p_card->nStatus, p_card->fBalance);
}
//��ѯ��
pList_card make()//����һ��������
{
	pList_card head = NULL;
	pList_card tail = NULL;
	head = (pList_card)malloc(sizeof(List_card));
	if (head == NULL)
		return NULL;//ͷ��������ڴ�ʧ��,����NULL
	head->next = NULL;
	tail = head;
	return head;
}
pList_card add_message(pList_card head,Card message_card)//��������ͷָ�룬card����Ϣ��ֵ���ݣ�
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
pList_card search_card(pList_card head, const char* pName)//Ѱ��Ŀ���㣬���ؽ��ָ�룬�Ҳ�������NULL
{
	pList_card p = head;
	int sign = 0;
	while (p->next != NULL)//��������
	{
		p = p->next;
		if (strcmp(&p->card.aName, pName) == 0)//�жϿ���
		{
			sign = 1;
			break;
		}
	}
	if (sign == 0)
		return NULL;
	else return p;
}
pList_card search_cards(pList_card head, const char* pName,int* pIndex)//ģ�����ң������½�����ͷ���ָ�룬�Ҳ�������NULL
{
	pList_card p = head,goal_head=NULL;
	goal_head = make();
	while (p->next != NULL)//��������
	{
		p = p->next;
		if (strstr(&p->card.aName,pName) != NULL)//�ж��Ƿ��йؼ���
		{
			(*pIndex)++;
			goal_head = add_message(goal_head, p->card);
		}
	}
	return goal_head;
}
void message2_card(const Card* pcard)//��ʾ��ѯ����Ϣ
{
	//printf("---��ѯ����Ϣ����---");
	char str[50], * format = "%Y-%m-%d %H:%M:%S";
	strftime(str, sizeof(str), format, localtime(&pcard->tLast));
	printf("����\t״̬\t���\t�ۼ�ʹ��\tʹ�ô���\t�ϴ�ʹ��ʱ��\n");
	printf("%s\t%d\t%.1f\t%.1f\t\t%d\t\t%s\n", pcard->aName, pcard->nStatus, pcard->fBalance, pcard->fTotalUse, pcard->nUseCount, str);
}
void disp_list(pList_card head)//�������������Ϣ
{
	pList_card p = head;
	while (p->next != NULL)
	{
		p = p->next;
		message2_card(&(p->card));
	}
}
void release_cardList(pList_card head)//�ͷ�����
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
//ע����
int do_annul()//ע��������
{
	char card_name[50], card_pwd[20], * pstr1, * pstr2;
	printf("�����뿨�ţ�����1~18����");
	scanf("%s", card_name);
	pstr1 = card_name;
	printf("���������루����1~8����");
	scanf("%s", card_pwd);
	pstr2 = card_pwd;
	Card goal_card, * pcard = NULL;
	pcard = validata(pstr1, pstr2);//��֤����������
	if (pcard == NULL)
		return 0;
	if (pcard->nStatus == 1)//�����ϻ��Ŀ��޷�ע��
	{
		printf("�ÿ������ϻ���");
		return 0;
	}
	goal_card = *pcard;
	float money = 0;
	money = goal_card.fBalance;
	int sign = money_status(pstr1, money, 1);//���������������Ѽ�¼�ļ�
	if (sign == 0)
	{
		printf("���Ѽ�¼��Ϣ����ʧ�ܣ�");
		return 0;
	}
	else
	{
		goal_card.fTotalUse -= goal_card.fBalance;//�ۼƽ��
		goal_card.fBalance = 0;//���
		goal_card.nUseCount++;//ʹ�ô���
		goal_card.tLast = time(NULL);//���ʹ��ʱ��
		goal_card.nDel = 1;//ɾ��״̬
	}
	pcard = &goal_card;
	char* pathcard = NULL;
	char path[100];
	strcpy(path, path_card(pcard->aName));//�����ļ�·��
	pathcard = path;
	int num = save_card(pcard, pathcard, "a");//���ע������Ϣ�����ĵ����ļ�
	if (num == 0)
		printf("������Ϣʧ�ܣ�");
	pList_card head = NULL;
	head = update_file(&goal_card);//�������п������ļ��иÿ�����Ϣ
	if (head == NULL)
	{
		printf("�ļ�����ʧ�ܣ�");
	}
	else
		release_cardList(head);
	message3_card(&goal_card, money);
	return 1;
}
void message3_card(const Card* pcard, const float money)//ע��������ʾ����Ϣ
{
	char str[50], * format = "%Y-%m-%d %H:%M:%S";
	strftime(str, sizeof(str), format, localtime(&pcard->tLast));
	printf("����\t�˷�\t���\t�ۼƽ��\tʹ��ʱ��\n");
	printf("%s\t%.1f\t%.1f\t%.1f\t\t%s\n", pcard->aName, money, pcard->fBalance, pcard->fTotalUse, str);
}
//�ϻ�
Card* do_logon(const char* pName, const char* pPwd)//�����ϻ���֤
{
	Card* pcard = NULL;
	Card goal_card;
	pcard = queryCard(pName);
	if (pcard == NULL)
	{
		printf("�����������");
		return NULL;
	}
	if (strcmp(pcard->aPwd, pPwd) != 0)
	{
		printf("�����������");
		return NULL;
	}
	if (pcard->nDel == 1)
	{
		printf("�ÿ��ѱ�ע����");
		return NULL;
	}
	goal_card = *pcard;
	//goal_card.nStatus = 1;//��ʾ�ϻ�
	goal_card.nUseCount++;//ʹ�ô���+1
	time_t time_now = time(NULL);
	goal_card.tLast = time_now;//�����ϴ�ʹ��ʱ��Ϊ�ϻ�ʱ��
	return &goal_card;
}
void message4_card(const Card* pcard)//�ϻ�����ʾ����Ϣ
{
	char str[50], * format = "%Y-%m-%d %H:%M:%S";
	strftime(str, sizeof(str), format, localtime(&pcard->tLast));
	printf("����\t���\t�ϻ�ʱ��\n");
	printf("%s\t%.1f\t%s\n", pcard->aName, pcard->fBalance, str);
}
Rule* bill_message()//��������ѡ��
{
	Rule rule;
	Allrule allrule, * pallrule = NULL;
	pallrule = &allrule;
	FILE* fp = NULL;
	fp = fopen(ALLBILL_PATH, "r");
	if (fp == NULL)
	{
		printf("�ļ���ʧ�ܣ�");
		return NULL;
	}
	if (fread(pallrule, sizeof(Allrule), 1, fp) == 0)
	{
		printf("�Ʒѱ�׼��ȡʧ�ܣ�");
		return NULL;
	}
	fclose(fp);
	rule.unit = allrule.Unit;//��С�Ʒѵ�Ԫ
	rule.charge = allrule.Charge;//ÿ���Ʒѵ�Ԫ����
	rule.day_charge = allrule.Day_charge;//�������
	rule.night_charge = allrule.Night_charge;//��ҹ����
	rule.amount = 0;
	int rate_type = -1;
	printf("��ѡ���������0-��ͨ��1-��ҹ��2-���죩��");
	do
	{
		scanf("%d", &rate_type);
		if (rate_type != 0 && rate_type != 1 && rate_type != 2)
			printf("�������\n���������룺");
	} while (rate_type != 0 && rate_type != 1 && rate_type != 2);
	rule.ratetype = rate_type;//�������
	rule.starttime = time(NULL);//���ѿ�ʼʱ��
	rule.endtime = 0;//���ѽ���ʱ��0
	rule.del = 0;//δɾ��-0
	return &rule;
}
char* path_billdata(const char* pname)//���Ѽ�¼��Ϣ·����
{
	char* path_bill = NULL;
	char str1[100] = "D:\\AMS\\AccountManagement\\billing_file\\", * str2 = "_fill.txt";
	strcat(str1, pname);
	strcat(str1, str2);
	path_bill = str1;
	return path_bill;
}
int bill_addto_file(const Rule* rule, const Card card)//������������Ϣ�����ļ�
{
	char path[100];
	strcpy(path, path_billdata(card.aName));
	int sign = save_bill(rule, path, "w");
	if (sign == 0)
		return 0;
	else return 1;
}
//�»�
Card* do_settle(const char* pName, const char* pPwd,float *pmoney)//�����»�������pmoney���ڷ������ѽ��
{
	Card* pcard = NULL;
	Card goal_card;
	time_t now_time = time(NULL);
	double diff_time = 0;
	pcard = queryCard(pName);
	if (pcard == NULL)
	{
		printf("�����������");
		return NULL;
	}
	if (strcmp(pcard->aPwd, pPwd) != 0)
	{
		printf("�����������");
		return NULL;
	}
	if (pcard->nDel == 1)
	{
		printf("�ÿ��ѱ�ע����");
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
		printf("�Ʒ���Ϣ�ļ���ʧ�ܣ�");
		return NULL;
	}
	if (fread(pbill, sizeof(Rule), 1, fp) == 0)
	{
		printf("�Ʒ���Ϣ��ȡʧ�ܣ�");
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
	*pmoney = bill_rule.amount;//���ѽ��
	if (bill_rule.amount > goal_card.fBalance)//�жϿ�����Ƿ��㹻
	{
		printf("�������㣡");
		return NULL;
	}
	else
	{
		goal_card.fBalance -= bill_rule.amount;//����������
		goal_card.nStatus = 0;//���¿�״̬��0-δ�ϻ�
		goal_card.nUseCount++;//ʹ�ô�����1
		goal_card.tLast = now_time;//���ʹ��ʱ�����
		bill_rule.del = 1;//ɾ����־��1-��ɾ��
	}
	int sign = money_status(goal_card.aName, bill_rule.amount, 2);//�����ѽ��������Ѽ�¼�ļ�
	if (sign == 0)
	{
		printf("���Ѽ�¼����ʧ�ܣ�");
		return NULL;
	}
	int sign_turnover = putin_turnover(bill_rule.amount);
	if (sign_turnover == 0)
	{
		printf("�����Ӫҵ���ļ�ʧ�ܣ�");
	}
	if (save_bill(&bill_rule, bill_path, "w") == 0)
	{
		printf("�ļ��мƷ���Ϣ����ʧ�ܣ�");
		return NULL;
	}
	return &goal_card;
}
void message5_card(const Card* pcard,const float money)//�»�����ʾ����Ϣ
{
	char str[50], * format = "%Y-%m-%d %H:%M:%S";
	strftime(str, sizeof(str), format, localtime(&pcard->tLast));
	printf("����\t����\t���\t�»�ʱ��\n");
	printf("%s\t%.1f\t%.1f\t%s\n", pcard->aName,money, pcard->fBalance, str);
}
//��ֵ
Card* validata(const char* pname, const char* ppwd)//��֤��������
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
int do_addmoney()//��ֵ��һϵ�в���
{
	char card_name[50], card_pwd[20], * pstr1, * pstr2;
	printf("�����뿨�ţ�����1~18����");
	scanf("%s", card_name);
	pstr1 = card_name;
	printf("���������루����1~8����");
	//scanf("%s", card_pwd);
	getchar();//���ջس���
	pstr2 = protect_pwd();//���뱣��
	strcpy(card_pwd, pstr2);
	pstr2 = card_pwd;
	Card goal_card, * pcard = NULL;
	pcard = validata(pstr1, pstr2);
	if (pcard == NULL)
		return 0;
	if (pcard->nDel == 1)
	{
		printf("�ÿ��ѱ�ע����");
		return 0;
	}
	goal_card = *pcard;
	float money = 0;
	printf("�������ֵ��");
	scanf("%f", &money);
	int sign = money_status(pstr1, money, 0);//����ֵ���������Ѽ�¼�ļ�
	if (sign == 0)
	{
		printf("���Ѽ�¼��Ϣ����ʧ�ܣ�");
		return 0;
	}
	else
	{
		goal_card.fBalance += money;//���
		goal_card.fTotalUse += money;//�ۼƽ��
		goal_card.nUseCount++;//ʹ�ô���
		goal_card.tLast = time(NULL);//���ʹ��ʱ��
	}
	pcard = &goal_card;
	char* pathcard = NULL;
	char path[100];
	strcpy(path, path_card(pcard->aName));//�����ļ�·��
	pathcard = path;
	int num = save_card(pcard, pathcard, "a");//��ӳ�ֵ��Ϣ�����ĵ����ļ�
	if (num == 0)
		printf("������Ϣʧ�ܣ�");
	pList_card head = NULL;
	head = update_file(&goal_card);//�������п������ļ��иÿ�����Ϣ
	if (head == NULL)
	{
		printf("�ļ�����ʧ�ܣ�");
	}
	else
		release_cardList(head);
	message6_card(&goal_card, money);
	return 1;
}
void message6_card(const Card* pcard, const float money)//��ֵ����ʾ����Ϣ
{
	char str[50], * format = "%Y-%m-%d %H:%M:%S";
	strftime(str, sizeof(str), format, localtime(&pcard->tLast));
	printf("����\t��ֵ\t���\t��ֵʱ��\n");
	printf("%s\t%.1f\t%.1f\t%s\n", pcard->aName, money, pcard->fBalance, str);
}
//�˷�
int do_refundmoney()//�˷ѵ�һϵ�в���
{
	char card_name[50], card_pwd[20], * pstr1, * pstr2;
	printf("�����뿨�ţ�����1~18����");
	scanf("%s", card_name);
	pstr1 = card_name;
	printf("���������루����1~8����");
	//scanf("%s", card_pwd);
	getchar();//���ջس���
	pstr2 = protect_pwd();//���뱣��
	strcpy(card_pwd, pstr2);
	pstr2 = card_pwd;
	Card goal_card, * pcard = NULL;
	pcard = validata(pstr1, pstr2);
	if (pcard == NULL)
		return 0;
	if (pcard->nDel == 1)
	{
		printf("�ÿ��ѱ�ע����");
		return 0;
	}
	goal_card = *pcard;
	float money = 0;
	printf("�������˷ѽ�");
	scanf("%f", &money);
	if (money > goal_card.fBalance)
	{
		printf("�˷ѽ�����");
		return 0;
	}
	int sign = money_status(pstr1, money, 1);//���˷ѽ��������Ѽ�¼�ļ�
	if (sign == 0)
	{
		printf("���Ѽ�¼����ʧ�ܣ�");
		return 0;
	}
	else
	{
		goal_card.fBalance -= money;//���
		goal_card.fTotalUse -= money;//�ۼƽ��
		goal_card.nUseCount++;//ʹ�ô���
		goal_card.tLast = time(NULL);//���ʹ��ʱ��
	}
	pcard = &goal_card;
	char* pathcard = NULL;
	char path[100];
	strcpy(path, path_card(pcard->aName));//�����ļ�·��
	pathcard = path;
	int num = save_card(pcard, pathcard, "a");//����˷���Ϣ�����ĵ����ļ�
	if (num == 0)
		printf("������Ϣʧ�ܣ�");
	pList_card head = NULL;
	head = update_file(&goal_card);//�������п������ļ��иÿ�����Ϣ
	if (head == NULL)
	{
		printf("�ļ�����ʧ�ܣ�");
	}
	else
		release_cardList(head);
	message7_card(&goal_card, money);
	return 1;
}
void message7_card(const Card* pcard, const float money)//�˷Ѻ���ʾ����Ϣ
{
	char str[50], * format = "%Y-%m-%d %H:%M:%S";
	strftime(str, sizeof(str), format, localtime(&pcard->tLast));
	printf("����\t�˷�\t���\t�˷�ʱ��\n");
	printf("%s\t%.1f\t%.1f\t%s\n", pcard->aName, money, pcard->fBalance, str);
}
//���Ѽ�¼
char* bill_manage_path(const char* pname)//���Ѽ�¼�����ļ�·��
{
	char* bill_manage_path = NULL;
	char str1[100] = "D:\\AMS\\AccountManagement\\billing_file\\bill_manage\\", * str2 = "_fee.txt";
	strcat(str1, pname);
	strcat(str1, str2);
	//bill_manage_path = str1;
	return str1;
}
int save_money_status(const Manage* manage, const char* money_path, const char* mode)//���������Ϣ���ļ�
{
	FILE* fp = NULL;
	char path[100];
	strcpy(path, money_path);
	fp = fopen(path, mode);
	if (fp == NULL)
	{
		printf("�ļ���ʧ�ܣ�");
		return 0;
	}
	size_t size = fwrite(manage, sizeof(Manage), 1, fp);
	fclose(fp);
	if (size == 0)
	{
		printf("��Ϣд��ʧ�ܣ�");
		return 0;
	}
	else return 1;
}
int money_status(const char* pname, const float money, const int operate)//���Ʒ���״̬��Ϣ
{
	Manage manage;
	strcpy(manage.cardName, pname);//����
	manage.operation = operate;//�������
	manage.money = money;//���
	manage.del = 0;
	manage.operationtime = time(NULL);
	char* ppath = NULL, money_path[100];
	ppath = bill_manage_path(pname);
	strcpy(money_path, ppath);
	int sign = save_money_status(&manage, money_path, "a");//����������Ϣ���ļ�
	if (sign == 0)
		return 0;
	else
		return 1;
}
pManage_list make_managelist()//�������Ѽ�¼������
{
	pManage_list head = NULL;
	pManage_list tail = NULL;
	head = (pManage_list)malloc(sizeof(Manage_list));
	if (head == NULL)
		return NULL;//ͷ��������ڴ�ʧ��,����NULL
	head->next = NULL;
	tail = head;
	return head;
}
pManage_list add_managelist(pManage_list head, Manage add_manage)//�����Ѽ�¼����β��ӽ��
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
void look_manage(Manage* manage)//չʾ�������е�һ�����Ѽ�¼
{
	char str[50], * format = "%Y-%m-%d %H:%M:%S";
	strftime(str, sizeof(str), format, localtime(&manage->operationtime));
	if (manage->operation == 0)
	{
		printf("��ֵ\tʱ��\n");
		printf("%.1f\t%s\n", manage->money, str);
	}
	else if (manage->operation == 1)
	{
		printf("�˷�\tʱ��\n");
		printf("%.1f\t%s\n", manage->money, str);
	}
	else
	{
		printf("����\tʱ��\n");
		printf("%.1f\t%s\n", manage->money, str);
	}
}
void disp_manage(pManage_list head)//�������Ѽ�¼����
{
	pManage_list p = head;
	while (p->next != NULL)
	{
		p = p->next;
		look_manage(&(p->manage));
	}
}
void release_managelist(pManage_list head)//�ͷ�����
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
int do_billrecord()//�������Ѽ�¼��ѯ����
{
	char card_name[50], card_pwd[20], * pstr1, * pstr2;
	printf("�����뿨�ţ�����1~18����");
	scanf("%s", card_name);
	pstr1 = card_name;
	printf("���������루����1~8����");
	//scanf("%s", card_pwd);
	getchar();//���ջس���
	pstr2 = protect_pwd();//���뱣��
	strcpy(card_pwd, pstr2);
	pstr2 = card_pwd;
	Card goal_card, * pcard = NULL;
	pcard = validata(pstr1, pstr2);
	if (pcard == NULL)
		return 0;
	goal_card = *pcard;
	char* ppath = NULL, fee_path[100];
	ppath = bill_manage_path(goal_card.aName);//���Ѽ�¼�ļ���·��
	strcpy(fee_path, ppath);
	Manage tool_manage;
	pManage_list head = make_managelist();
	FILE* fp;
	fp = fopen(fee_path, "r");
	if (fp == NULL)
	{
		printf("�ļ���ʧ�ܣ�");
		return 0;
	}
	while (1)
	{
		if (fread(&tool_manage, sizeof(Manage), 1, fp) == 0)//��ȡ�ļ���Ϣ���ṹ��
		{
			break;
		}
		head = add_managelist(head, tool_manage);//���ṹ����Ϣ��������
	}
	fclose(fp);//�ر��ļ�
	disp_manage(head);//����������Ϣ
	release_managelist(head);//�ͷ�����
	return 1;
}
//�������
char* protect_pwd()//���뱣��
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
+ card_file.c�ļ�
```c
#pragma warning(disable:4996)
#define _CRT_SECURE_NO_WARNINGS
#pragma once
#include<stdio.h>
#include<stdlib.h>
#include<time.h>
#include<string.h>
#include"service.h"
#define PATH "D:\\AMS\\AccountManagement\\data\\card_data.txt"//����Ϣ·��
#define ALLBILL_PATH "D:\\AMS\\AccountManagement\\billing_file\\bill_message\\allbill_rule.txt"//�Ʒѱ�׼��Ϣ����·��
#define NUM 100
//��ӿ���غ���
int save_card(const Card* p_card, const char* p_path, const char* mode)//��������Ϣ���浽�ļ���
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
//��ѯ����غ���
int queryCard1(const char* pName)//ʹ�ýṹ�徫ȷ��ѯ
{
	extern Card aCard[NUM];
	FILE* fp = NULL;
	fp = fopen(PATH, "rb");
	if (fp == NULL)
	{
		printf("�ļ���ʧ�ܣ�");
		exit(0);
	}
	int searchnum = -1;
	for (int i = 0; i < NUM; i++)
	{
		if (fread(&aCard[i], sizeof(Card), 1, fp) == 0)
		{
			//printf("�ļ���ȡʧ�ܣ�\n");
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
Card* queryCard(const char* pName)//ʹ�����������Ϣ����ȷ���ң�
{
	FILE* fp;
	fp = fopen(PATH, "rb");//���ļ�
	if (fp == NULL)
	{
		printf("�ļ���ʧ�ܣ�");
		exit(0);
	}
	pList_card head = NULL, p = NULL;
	head = make();
	Card tool_card, goal_card;
	while (1)
	{
		if (fread(&tool_card, sizeof(Card), 1, fp) == 0)//��ȡ�ļ���Ϣ���ṹ��
		{
			break;
		}
		head = add_message(head, tool_card);//���ṹ����Ϣ��������
	}
	fclose(fp);//�ر��ļ�
	p = search_card(head, pName);//Ѱ��Ŀ����
	if (p == NULL)
		return NULL;
	goal_card = p->card;
	release_cardList(head);//�ͷ�����
	return &goal_card;
}
pList_card* queryCards(const char* pName, int* pIndex)//ʹ������ģ�����ҿ���Ϣ
{
	FILE* fp;
	fp = fopen(PATH, "rb");//���ļ�
	if (fp == NULL)
	{
		printf("�ļ���ʧ�ܣ�");
		exit(0);
	}
	pList_card head = NULL,goal_head=NULL;
	head = make();
	Card tool_card, goal_card;
	while (1)
	{
		if (fread(&tool_card, sizeof(Card), 1, fp) == 0)//��ȡ�ļ���Ϣ���ṹ��
		{
			break;
		}
		head = add_message(head, tool_card);//���ṹ����Ϣ��������
	}
	fclose(fp);//�ر��ļ�
	goal_head = search_cards(head, pName, pIndex);//����ѯ��Ϣ����Ŀ������
	release_cardList(head);//�ͷ�����
	return goal_head;//����Ŀ������ͷָ��
}
//�ϻ���غ���
int insert_newfile(const pList_card head, const char* p_path)//����������Ϣд���ļ�
{
	pList_card p = head->next;
	Card tool_card;
	tool_card = p->card;
	int sign = save_card(&tool_card, PATH, "w");//����ļ���ԭ����������д���һ�������Ϣ
	if (sign == 0)
	{
		//printf("����д����Ϣʧ�ܣ�");
		return 0;
	}
	while (p->next != NULL)
	{
		p = p->next;
		tool_card = p->card;
		sign = save_card(&tool_card, PATH, "a");//��׷����ʽ��������д���ļ�
		if (sign == 0)
		{
			//printf("����д����Ϣʧ�ܣ�");
			return 0;
		}
	}
	return 1;//д��ɹ�����1�����򷵻�0
}
pList_card update_file(const Card* pcard)//��ԭ�ļ���Ϣ�������������������Ϣ��������д���ļ�
{
	FILE* fp = NULL;
	fp = fopen(PATH, "rb");//���ļ�
	if (fp == NULL)
	{
		//printf("�ļ���ʧ�ܣ�");
		return NULL;
	}
	pList_card head = NULL, p = NULL;
	head = make();
	Card tool_card;
	while (1)
	{
		if (fread(&tool_card, sizeof(Card), 1, fp) == 0)//��ȡ�ļ���Ϣ���ṹ��
		{
			break;
		}
		head = add_message(head, tool_card);//���ṹ����Ϣ��������
	}
	fclose(fp);//�ر��ļ�
	p = search_card(head, pcard->aName);//Ѱ��Ŀ����
	p->card = (*pcard);//�޸Ľ����Ϣ
	int sign = insert_newfile(head, PATH);
	if (sign == 0)
	{
		//printf("�ļ�����ʧ�ܣ�");
		return NULL;
	}
	return head;//��������ͷ��㣬ʧ�ܷ���NULL
}
//�»���غ���
int save_bill(const Rule* p_bill, const char* p_path, const char* mode)//���Ʒѵ���Ϣ���浽�ļ���
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
+ manage.c�ļ�
```c
#pragma warning(disable:4996)
#define _CRT_SECURE_NO_WARNINGS
#pragma once
#include<stdio.h>
#include<stdlib.h>
#include<time.h>
#include<string.h>
#include"service.h"
#define ALLBILL_PATH "D:\\AMS\\AccountManagement\\billing_file\\bill_message\\allbill_rule.txt"//�Ʒѱ�׼��Ϣ����·��
#define MANAGER_PATH "D:\\AMS\\AccountManagement\\data\\manager_data.txt"//����Ա��Ϣ����·��
#define TURNOVER_PATH "D:\\AMS\\AccountManagement\\billing_file\\bill_message\\turnover.txt"//Ӫҵ�ܶ��ļ�·��
//#define MANAGE_PATH "D:\\AMS\\AccountManagement\\data\\manage_data.txt"
int make_allrule()//����±�׼���ļ�
{
	Allrule totalrule;
	printf("��������С�Ʒѵ�Ԫ(����)��");
	scanf("%d", &totalrule.Unit);
	printf("������ÿ��Ԫʱ��ķ��ã�");
	scanf("%f", &totalrule.Charge);
	printf("�����������ã�");
	scanf("%f", &totalrule.Day_charge);
	printf("�������ҹ���ã�");
	scanf("%f", &totalrule.Night_charge);
	FILE* fp = NULL;
	fp = fopen(ALLBILL_PATH, "w");//���ļ���ֻ�����ı���
	if (fp == NULL)
		return 0;
	size_t size = fwrite(&totalrule, sizeof(Allrule), 1, fp);
	if (size == 0)
	{
		printf("�Ʒѱ�׼д���ļ�ʧ�ܣ�");
		return 0;
	}
	fclose(fp);
	display_allrule();
	return 1;
}
void display_allrule()//��ʾ�Ʒѱ�׼��Ϣ
{
	Allrule totalrule;
	FILE* fp = NULL;
	fp = fopen(ALLBILL_PATH, "r");
	if (fp == NULL)
	{
		printf("�ļ���ʧ�ܣ�");
	}
	if (fread(&totalrule, sizeof(Allrule), 1, fp) == 0)
		printf("�ļ���ȡʧ�ܣ�");
	fclose(fp);
	printf("---�Ʒѱ�׼��Ϣ����---\n");
	printf("�Ʒѵ�Ԫ\t��Ԫ����\t�������\t��ҹ����\n");
	printf("%d\t\t%.2f\t\t%.2f\t\t%.2f\n", totalrule.Unit, totalrule.Charge, totalrule.Day_charge, totalrule.Night_charge);
}
int add_manager()//����¹���Ա
{
	Manager manager;
	printf("���������Ա����");
	scanf("%s", manager.name);
	printf("���������룺");
	scanf("%s", manager.pwd);
	manager.privilge = 1;
	manager.del = 0;
	FILE* fp = NULL;
	fp = fopen(MANAGER_PATH, "ab");
	if(fp==NULL)
	{
		printf("�ļ���ʧ�ܣ�");
		return 0;
	}
	size_t size = fwrite(&manager, sizeof(Manager), 1, fp);
	fclose(fp);
	if (size == 0)
	{
		printf("����Ա���ʧ�ܣ�");
		return 0;
	}
	else
	{
		printf("����Ա��ӳɹ���");
		return 1;
	}
}
pList_manager make_manager()//����һ��������(����Ա)
{
	pList_manager head = NULL;
	pList_manager tail = NULL;
	head = (pList_manager)malloc(sizeof(pList_manager));
	if (head == NULL)
		return NULL;//ͷ��������ڴ�ʧ��,����NULL
	head->next = NULL;
	tail = head;
	return head;
}
pList_manager add_manager_message(pList_manager head, Manager message)//��������ͷָ�룬manager����Ϣ��ֵ���ݣ�
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
pList_manager search_manager(pList_manager head, const char* pName)//Ѱ��Ŀ���㣬���ؽ��ָ�룬�Ҳ�������NULL
{
	pList_manager p = head;
	int sign = 0;
	while (p->next != NULL)//��������
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
void release_managerList(pList_manager head)//�ͷŹ���Ա����
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
Manager* queryManager(const char* pName)//ʹ������ȷ���ҹ���Ա��Ϣ
{
	FILE* fp;
	fp = fopen(MANAGER_PATH, "rb");//���ļ���ֻ���������ƣ�
	if (fp == NULL)
	{
		printf("�ļ���ʧ�ܣ�");
		return NULL;
	}
	pList_manager head = NULL, p = NULL;
	head = make_manager();//����������
	Manager tool_manager, goal_manager;
	while (1)
	{
		if (fread(&tool_manager, sizeof(Manager), 1, fp) == 0)//��ȡ�ļ���Ϣ���ṹ��
		{
			break;
		}
		head = add_manager_message(head, tool_manager);//���ṹ����Ϣ��������
	}
	fclose(fp);//�ر��ļ�
	p = search_manager(head, pName);//Ѱ��Ŀ����
	if (p == NULL)
		return NULL;
	goal_manager = p->manager;
	release_managerList(head);//�ͷ�����
	return &goal_manager;
}
int do_manage(const char* pname, const char* ppwd)//����Ա��֤���޸ļƷѱ�׼
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
		printf("�Ʒѱ�׼�޸ĳɹ���");
	else
		printf("�Ʒѱ�׼�޸�ʧ�ܣ�");
	return 1;
}
//Ӫҵ����غ���
pTurnoverlist make_turnoverlist()//����Ӫҵ�������
{
	pTurnoverlist head = NULL;
	pTurnoverlist tail = NULL;
	head = (pTurnoverlist)malloc(sizeof(Turnoverlist));
	if (head == NULL)
		return NULL;//ͷ��������ڴ�ʧ��,����NULL
	head->next = NULL;
	tail = head;
	return head;
}
pTurnoverlist add_turnover(pTurnoverlist head, Turnover add_turnover)//������β���������Ϣ
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
void release_turnoverlist(pTurnoverlist head)//�ͷ�����
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
pTurnoverlist file_putin_turnoverlist()//���ļ���������Ϣ��������
{
	FILE* fp = NULL;
	fp = fopen(TURNOVER_PATH, "r");//ֻ��
	if (fp == NULL)
	{
		printf("�ļ���ʧ�ܣ�");
		return 0;
	}
	pTurnoverlist head = make_turnoverlist();//����������
	Turnover tool_turnover;
	while (1)
	{
		if (fread(&tool_turnover, sizeof(Turnover), 1, fp) == 0)//��ȡ�ļ���Ϣ���ṹ��
		{
			break;
		}
		head = add_turnover(head, tool_turnover);//���ṹ����Ϣ��������
	}
	fclose(fp);//�ر��ļ�
	return head;
}
int putin_turnover(const float money)//���µ�Ӫҵ��д���ļ���
{
	Turnover turnover;
	turnover.money = money;
	turnover.time = time(NULL);
	FILE* fp = NULL;
	fp = fopen(TURNOVER_PATH, "a");//β�������Ϣ
	size_t size = fwrite(&turnover, sizeof(Turnover), 1, fp);
	fclose(fp);
	if (size == 0)
	{
		printf("Ӫҵ��д���ļ�ʧ�ܣ�");
		return 0;
	}
	else
		return 1;
}
int view_turnover(const char* pname, const char* ppwd)//�鿴Ӫҵ�ܶ�
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
	printf("Ӫҵ�ܶ�\t�鿴ʱ��\n");
	printf("%.1f\t\t%s\n", allmoney, str);
	return 1;
}
```
+ menu.h�ļ�
```c
#ifndef MENU_H
#define MENU_H

void outputMenu();  //��������˵�����
void output_selectnum(int);  //���������ѡ�˵����
void add();  //������ӿ�����
void query();  //������ѯ������
void annul();  //����ע��������
void logon();  //�����ϻ�����
void settle();  //�����»�����
void addMoney();  //������ֵ����
void refundMoney();  //�����˷Ѻ���
void billRecord();  //�������Ѽ�¼��ѯ����
//void exitApp();  //�����˳�Ӧ�ó�����
void manage();   //����������
#endif
```
+ service.h�ļ�
```c
#ifndef SERVICE
//���ṹ��
typedef struct Card
{
	char aName[18];  //���ţ�����Ϊ�գ�����Ϊ1~18���ַ�
	char aPwd[8];  //���룬����Ϊ�գ�����Ϊ1~8���ַ�
	int nStatus;  //��״̬��0-δ�ϻ���1-�����ϻ���2-��ע����3-ʧЧ
	time_t tStart;  //����ʱ��
	time_t tEnd;  //��ֹʱ��
	float fTotalUse;  //�ۼƽ��
	time_t tLast;  //���ʹ��ʱ��
	int nUseCount;  //ʹ�ô���
	float fBalance;  //���
	int nDel;  //ɾ����־��0-δɾ����1-��ɾ��
}Card;
//�Ʒѱ�׼��Ϣ
typedef struct bill_rule
{
	time_t starttime;  //��ʼʱ��
	time_t endtime;  //����ʱ��
	float amount;  //���ѽ��
	int unit;  //��С�Ʒѵ�Ԫ�����ӣ�
	float charge;  //ÿ���Ʒѵ�Ԫ���շ�
	float night_charge;  //��ҹ����
	float day_charge;  //�������
	int ratetype;  //�շ����0-��ͨ��1-��ҹ��2-����
	int del;  //ɾ����־��0-δɾ����1-��ɾ��
}Rule;
//�����׼
typedef struct all_rule
{
	int Unit;//��С�Ʒѵ�Ԫ
	float Charge;//ÿ���Ʒѵ�Ԫ�շ�
	float Day_charge;//�������
	float Night_charge;//��ҹ����
}Allrule;
//��ֵ�˷���Ϣ
typedef struct bill_manage
{
	char cardName[18];  //����
	time_t operationtime;  //����ʱ��
	int operation;  //�������0-��ֵ��1-�˷�;2-�»�
	float money;  //����
	int del;  //ɾ����־��0-δɾ����1-��ɾ��
}Manage;
//����Ա��Ϣ
typedef struct manager
{
	char name[18];  //�û���
	char pwd[8];  //����
	int privilge;  //Ȩ�޵ȼ�
	int del;  ////ɾ����־��0-δɾ����1-��ɾ��
}Manager;
//����Ա������
typedef struct List_manager
{
	Manager manager;
	struct List_manager* next;
}List_manager,*pList_manager;
//��������
typedef struct List_card   
{
	Card card;
	struct List_card* next;
}List_card,*pList_card;
//���Ѽ�¼���
typedef struct managelist
{
	Manage manage;
	struct managelist* next;
}Manage_list, * pManage_list;
//Ӫҵ��ṹ��
typedef struct turnover
{
	float money;//Ӫҵ����
	time_t time;//����ʱ��
}Turnover;
//Ӫҵ����
typedef struct turnover_list
{
	Turnover turnover;
	struct turnover_list* next;
}Turnoverlist, * pTurnoverlist;
//��ӿ���غ���
void input_card(Card* card);//���������Ϣ
char* path_card(const char* pname);//�����ļ�·����
int save_card(const Card* p_card, const char* p_path,const char* mode);//���濪����Ϣ���ļ�
void message1_card(const Card* p_card);//��ʾ������Ϣ
//��ѯ����غ���
void message2_card(const Card* pcard);//��ʾ��ѯ����Ϣ
int queryCard1(const char* pName);//ʹ������׼ȷ����
pList_card make();//����������
pList_card add_message(pList_card head, Card message_card);//��������ͷָ�룬card����Ϣ��ֵ���ݣ�
void release_cardList(pList_card head);//�ͷ�����
pList_card search_card(pList_card head, const char* pName);
Card* queryCard(const char* pName);//ʹ������׼ȷ����
void disp_list(pList_card head);//�������������Ϣ
pList_card search_cards(pList_card head, const char* pName, int* pIndex);//ģ�����ң������½�����ͷ���ָ�룬�Ҳ�������NULL
pList_card* queryCards(const char* pName, int* pIndex);//ʹ������ģ�����ҿ���Ϣ
//ע����
int do_annul();//ע��������
void message3_card(const Card* pcard, const float money);//ע��������ʾ����Ϣ
//�ϻ���غ���
Card* do_logon(const char* pName, const char* pPwd);//�����ϻ���֤
void message4_card(const Card* pcard);//�ϻ�����ʾ����Ϣ
int insert_newfile(const pList_card head, const char* p_path);//����������Ϣд���ļ�
pList_card update_file(const Card* pcard);//���ļ���Ϣ�������������������Ϣ��������д���ļ�
Rule* bill_message();//��������ѡ��
char* path_billdata(const char* pname);//���Ѽ�¼��Ϣ·����
int bill_addto_file(const Rule* rule, const Card card);//������������Ϣ�����ļ�
int save_bill(const void* p_bill, const char* p_path, const char* mode);//���Ʒѵ���Ϣ���浽�ļ���
//�»���غ���
Card* do_settle(const char* pName, const char* pPwd,float *pmoney);//�����»�������pmoney���ڷ������ѽ��
void message5_card(const Card* pcard,const float money);//�»�����ʾ����Ϣ
//��ֵ��غ���
Card* validata(const char* pname, const char* ppwd);//��֤��������
int do_addmoney();//��ֵ��һϵ�в���
void message6_card(const Card* pcard, const float money);//��ֵ����ʾ����Ϣ
//�˷���غ���
int do_refundmoney();//��ֵ��һϵ�в���
void message7_card(const Card* pcard, const float money);//�˷Ѻ���ʾ����Ϣ
//���Ѽ�¼��غ���
char* bill_manage_path(const char* pname);//���Ѽ�¼�����ļ�·��
int save_money_status(const Manage* manage, const char* money_path, const char* mode);//���������Ϣ���ļ�
int money_status(const char* pname, const float money, const int operate);//���Ʒ���״̬��Ϣ
pManage_list make_managelist();//�������Ѽ�¼������
pManage_list add_managelist(pManage_list head, Manage add_manage);//�����Ѽ�¼����β��ӽ��
void look_manage(Manage* manage);//չʾ�������е�һ�����Ѽ�¼
void disp_manage(pManage_list head);//�������Ѽ�¼����
void release_managelist(pManage_list head);//�ͷ�����
int do_billrecord();//�������Ѽ�¼��ѯ����
//Ӫҵ����غ���
pTurnoverlist make_turnoverlist();//����Ӫҵ�������
pTurnoverlist add_turnover(pTurnoverlist head, Turnover add_turnover);//������β���������Ϣ
void release_turnoverlist(pTurnoverlist head);//�ͷ�����
pTurnoverlist file_putin_turnoverlist();//���ļ���������Ϣ��������
int putin_turnover(const float money);//���µ�Ӫҵ��д���ļ���
int view_turnover(const char* pname, const char* ppwd);//�鿴Ӫҵ�ܶ�
//����Ա��غ���
int add_manager();//����¹���Ա
pList_manager make_manager();//����һ��������(����Ա)
pList_manager add_manager_message(pList_manager head, Manager message);//��������ͷָ�룬manager����Ϣ��ֵ���ݣ�
pList_manager search_manager(pList_manager head, const char* pName);//Ѱ��Ŀ���㣬���ؽ��ָ�룬�Ҳ�������NULL
void release_managerList(pList_manager head);//�ͷŹ���Ա����
Manager* queryManager(const char* pName);//ʹ������ȷ���ҹ���Ա��Ϣ
int do_manage(const char* pname, const char* ppwd);//����Ա��֤���޸ļƷѱ�׼
int make_allrule();//����±�׼���ļ�
void display_allrule();//��ʾ�Ʒѱ�׼��Ϣ
//����
char* protect_pwd();//���뱣��
#define SERVICE
#endif
```
