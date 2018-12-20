/* 创建BST的C代码实现 */
 
#include <stdio.h>
#include <stdlib.h>
 
typedef int Elemtype;
 
typedef struct BiTNode{
	Elemtype data;
	struct BiTNode *lchild, *rchild;
}BiTNode, *BiTree;
 
//在给定的BST中插入结点，其数据域为element
int BSTInsert( BiTree *t, Elemtype element )
{
	if( NULL == *t ) {
		(*t) = (BiTree)malloc(sizeof(BiTNode));
		(*t)->data = element;
		(*t)->lchild = (*t)->rchild = NULL;
		return 1;
	}
 
	if( element == (*t)->data )
		return 0;
 
	if( element < (*t)->data )
		return BSTInsert( &(*t)->lchild, element );
 
	return BSTInsert( &(*t)->rchild, element );
}
 
//创建BST
void CreateBST( BiTree *t, Elemtype *a, int n )
{
	(*t) = NULL;
	for( int i=0; i<n; i++ )
		BSTInsert( t, a[i] );
}
 
//中序遍历打印BST
void PrintBST( BiTree t )
{
	if( t ) {
		PrintBST( t->lchild );
		printf("%d ", t->data);
		PrintBST( t->rchild );
	}
}
 
int main()
{
	int n;
	int *a;
	BiTree t;
 
	printf("请输入二叉查找树的结点数:\n");
	scanf("%d", &n);
 
	a = (int *)malloc(sizeof(int)*n);
	printf("请输入而查找树的结点:\n");
	for( int i=0; i<n; i++ )
		scanf("%d", &a[i]);
 
	CreateBST( &t, a, n );
	printf("该BST的中序遍历结果为:\n");
	PrintBST( t );
	printf("\n");
 
	return 0;
}
