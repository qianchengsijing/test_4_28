# test_4_28
#include <stdio.h>
#include <stdlib.h>
//队列的链式存储
typedef struct LinkNode
{
	ElemType data;
	struct LinkNode* next;
}LinkNode;
typedef struct
{
	LinkNode* front,* rear;
}LinkQueue;
//初始化(带头结点）
void InitQueue(LinkQueue &Q)
{
	Q.front = Q.rear = (LinkNode*)malloc(sizeof(LinkNode));//创建头结点
	Q.front->next = NULL;
}
//初始化(不带头结点）
void InitQueue(LinkQueue &Q)
{
	Q.front = NULL;
	Q.rear = NULL;
}
//判空
bool IsEmpty(LinkQueue Q)
{
	if(Q.rear == Q.front)
		return true;
	else
		return false;
}
//入队（带头结点）
void EnQueue(LinkQueue &Q,ElemType x)
{
	LinkNode* s = (LinkNode*)malloc(sizeof(LinkNode));
    s->data = x;
	s->next = NULL;
    Q.rear->next = s;
	Q.rear = s;
}
//入队（不带头结点）
void EnQueue(LinkQueue &Q,ElemType x)
{
	LinkNode* s = (LinkNode*)malloc(sizeof(LinkNode));
    s->data = x;
	s->next = NULL;
	if(Q.rear == NULL)
	{
		Q.rear = s;
		Q.front = s;
	}
	else
	{
		Q.rear->next = s;
	    Q.rear = s;
	}
}
//出队（带头结点）
bool DeQueue(LinkQueue &Q,ElemType &x)
{
	if(Q.front == Q.rear)
		return false;
	LinkNode* p = Q.front->next;
	x = p->data;
	Q.front->next = p->next;
	if(Q.rear == p)//最后一个元素出队
		Q.rear = Q.front;
	free(p);//释放p的空间
	return true;
}
//出队（不带头结点）
bool DeQueue(LinkQueue &Q,ElemType &x)
{
	if(Q.front == Q.rear)
		return false;
	LinkNode* p = Q.front;
	x = p->data;
	Q.front = p->next;
	if(Q.rear == p)
	{
		Q.front = NULL;
		Q.rear = NULL;
	}
	free(p);
	return true;
}
void testLinkQueue()
{
	LinkQueue Q;
	InitQueue(Q);
	EnQueue(&Q,x);
	DeQueue(&Q,&x);
	IsEmpty(Q);
}
