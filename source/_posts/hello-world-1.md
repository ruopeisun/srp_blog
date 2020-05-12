---
title: 测试各种markdown语法
date: 2020-05-08 15:03:29
tags:
  - Markdown
  - Blog
categories: Markdown
description: Markdown语法测试
cover: https://raw.githubusercontent.com/ruopeisun/CDN/master/img/fgo15.png
---

# This is a test. 

这是一个关于markdown语法的测试


## 字体示例

**粗体字** 
*斜体字*
***又粗又斜*** 
~~这是被删掉的字~~

## 引用示例

>本文引用自xxxxx
>>>>多级引用示例

## 换行示例

----

## 图片示例

![fgo图片](https://cdn.jsdelivr.net/gh/ruopeisun/CDN@1.0/img/fgo5.png "本图片用作博客文章封面")

## 超链接示例

[这是一个测试超链接](https://www.baidu.com "他定向至百度")

[这是另外一个超链接](https://github.com/ruopeisun "他定向至我的github")

## 接下来是列表

### 无序列表

- 列表1
* 列表2
+ 列表3

----

### 有序列表

1. list one
2. list two
3. [list three](https://srprpr.ga)

---

#### 列表嵌套

- 一级列表（无序）
   - 二级列表（无序）
- 一级列表2
	- 二级列表1
	- 二级列表2
	- 二级列表3

---

## 表格

姓名|身份|排行
--|:--:|--:
szl|巨佬|1
zch|巨佬|1
我|菜鸡|1145141919810

## 代码

### 单行代码

`public static void main(String args[]);`

### 多行代码

>本代码摘自本人程序设计II第六周**递归和栈**作业的第二题
~~写的真工整(划掉)~~

```C++
#include <stdio.h>
#include <stdlib.h>
#include <iostream>

int RecursionTime = 0;

using namespace std;

struct FileInfo
{
	/*
	*	It contains a pointer to sub-dirs, and a string array to files.
	*	Also a name for dir, two int variable records the number of Dirs and Files.
	*/
	FileInfo *Dir[100];
	string File[100];
	string _name;
	int nDirNum;
	int nFileNum;
};

void _sort(string sString[], int slength)
{
	/*
	*	make the array in dictionary order. 
	*/
	for(int i = 0; i <= slength - 1; i++)
	{
		for(int j = i; j <= slength - 1; j++)
		{
			if(sString[i] > sString[j])
			{
				string temp;
				temp = sString[i];
				sString[i] = sString[j];
				sString[j] = temp;
			}
		}
	}
	return;
}

void __sort(FileInfo *fileinfo)
{
	/*
	*	make files in fileinfo in dictionary order.
	*/
	_sort(fileinfo->File, fileinfo->nFileNum);
	return;
}

bool Read(FileInfo *dir)
{
	/*
	*	This function reads the text from cmd and put the infomation into a tree dir.
	*
	*	When there is another group of data, it returns true to continue.
	*	If not, it return false to end the program.
	*/
	
	string name;
	int num1 = 0,num2 = 0;
	while(1)
	{
/*		scanf("%s", name);*/ cin>>name;
		switch(name[0])
		{
			case 'f':
				dir->File[num1++] = name;
				break;
			case 'd':
				dir->Dir[num2++] = new FileInfo;
				dir->Dir[num2 - 1]->_name = name;
				Read(dir->Dir[num2 - 1]);
				break;
			case ']':
				dir->nDirNum = num2;
				dir->nFileNum = num1;
				__sort(dir);
				return true;//When ended,sort dir and put num1 and num2 to dir as the num of files and dirs.
			case '*':
				dir->nDirNum = num2;
				dir->nFileNum = num1;
				__sort(dir);
				return true;
			case '#':
				return false;
		}
	}
}

void Write(FileInfo *fileinfo, int nRecurTime)
{
	/*
	*	Dealing with the data from fileinfo.
	*	dir and file output separately.	
	*/
	
		
	for(int i = 0; i < fileinfo->nDirNum; i++)
	{
		for(int j = 0; j <= nRecurTime; j++)
		{
			printf("|     ");
		}
		printf("%s", fileinfo->Dir[i]->_name.c_str());
		putchar('\n');
		Write(fileinfo->Dir[i], nRecurTime + 1);
	}
	for(int i = 0; i < fileinfo->nFileNum; i++)
	{
		for(int j = 0; j < nRecurTime; j++)
		{
			printf("|     ");
		}
		printf("%s", fileinfo->File[i].c_str());
		putchar('\n');
	}
	delete fileinfo;
	return;
}

int main(void)
{
	//Set of Data
	int num = 1;
	
	//input and output
	while(true)
	{
		FileInfo *fileinfo = new FileInfo;
		fileinfo->_name = "ROOT";
		if(Read(fileinfo))//When read #, return false and then exit.
		{
			printf("DATA SET %d:", num++);
			putchar('\n');
			printf("ROOT"); 
			putchar('\n');
			Write(fileinfo, 0);
			putchar('\n');
		}
		else
		{
			putchar('\n');
			return 0;
		}
		
	}
//	fclose(stdin);
//	fclose(stdout);
}
```

大概就这么多内容，先全记住语法再说。

---
