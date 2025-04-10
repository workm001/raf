```c
#include <stdio.h>
#include <stdlib.h>

struct node{
	int data;
	struct node *next;
};

void linkListTraversal(struct node *ptr){
	while(ptr != NULL){
		printf("%d ", ptr->data);
		ptr = ptr->next;
	}
}
int main(){
	
	struct node *first;
	struct node *secound;
	struct node *third;
	
	first  = (struct node *) malloc (sizeof(struct node));
	secound = (struct node *) malloc (sizeof(struct node));
	third = (struct node *) malloc(sizeof(struct node));
	
	first->data = 111;
	first->next = secound;
	
	secound->data = 222;
	secound->next = third;
	
	third->data = 333;
	third->next = NULL;
	
	linkListTraversal(first);
	
	return 0;
}

```