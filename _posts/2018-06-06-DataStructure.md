---
layout: post
title: Data Structure Report !
---
오늘은 자료구조의 선택,버블,삽입,기수 정렬과 
순차, 이진 검색 코드를 이론을 토대로 구현해보았다. 
삽입 정렬은 Linked List로 구현하였고 
삽입 정렬을 제외한 코드는 배열로 구현하였다.

#include <stdio.h>
typedef struct node {
	int data;
	struct node * left;
	struct node * right;
}node;
node* NewNode(int data) {
	node* newnode = (node*)malloc(sizeof(node));
	newnode->data = data;
	newnode->left = NULL;
	newnode->right = NULL;
	return newnode;
}
node* LinkingNode(node**Link) {

	int i;
	for (i = 0; i < 8; i++) {
		if(i == 0){
			Link[i]->right = Link[i + 1];
		}
		else if (i == 7) {
			Link[i]->left = Link[i - 1];
			return Link[0];
		}
		else {
			Link[i]->left = Link[i - 1];
			Link[i]->right = Link[i + 1];
		}
	}
}
void SelectionSort(int* data) {
	printf("\nSelection Sorting \n");
	printf("before : %d,%d,%d,%d,%d,%d,%d,%d\n\n",  data[0], data[1], data[2], data[3], data[4], data[5], data[6], data[7]);
	int i, j;
	int temp;
	for (i = 0; i < 8; i++) {
		int min = data[i];
		int minnum = i;
		for (j = i; j < 8; j++) {
			if (min > data[j]) {
				min = data[j];
				minnum = j;
			}
		}
		temp = min;
		data[minnum] = data[i];
		data[i] = min;
		
		
		printf("Path %d>> [%d <-> %d]",i+1,data[minnum],data[i]);
		if (data[minnum] == data[i])printf(" 변경없음\n");
		else printf("\n");

		
		
		printf("\t %d,%d,%d,%d,%d,%d,%d,%d\n\n", data[0], data[1], data[2], data[3], data[4], data[5], data[6], data[7]);
	}
	printf("end\t20133105 이재원\n");
}
void BubbleSort(int* data) {
	printf("\nBubble Sorting \n");
	printf("before : %d,%d,%d,%d,%d,%d,%d,%d\n", data[0], data[1], data[2], data[3], data[4], data[5], data[6], data[7]);
	int i = 0;
	int end = 7;
	int temp2,temp;
	printf("Path 1 >> \n");
	while(1){
		if (i == end) {
			i = 0;
			end--;
			printf("Path %d >>\n", 8 - end);
			continue;
		}
		else if (data[i] > data[i + 1]) {
			temp = data[i];
			temp2 = data[i+1];
			data[i] = temp2;
			data[i+1] = temp;
			i++;
			printf("\t%d,%d,%d,%d,%d,%d,%d,%d\n", data[0], data[1], data[2], data[3], data[4], data[5], data[6], data[7]);
			continue;
		}
		else {
			printf("\t%d,%d,%d,%d,%d,%d,%d,%d 변동 없음\n", data[0], data[1], data[2], data[3], data[4], data[5], data[6], data[7]);
			i++;
		}

		if (end == 1)break;
	}
	printf("\nend\t20133105 이재원\n");
}
void InsertSort(node* IS, node* CS) {
	
	node*temp = IS;
	while (temp->left != NULL) {
		temp = temp->left;
	}
	printf(">>");
	for (int i = 0; i < 8; i++) {
		printf("%d ", temp->data);
		temp = temp->right;
	}
	printf("\n");

	if (CS == NULL) return;

	else if (CS->data > IS->data) {
		InsertSort(CS, CS->right);
		return;
	}
	else if (CS->data < IS->data) {
		if (IS->left == NULL) {

			node*target = IS;
			node*CSLeft = CS->left;
			node*CSRight = CS->right;
			target->left = CS;
			CSLeft->right = CSRight;
			CSRight->left = CSLeft;
			CS->left = NULL;
			CS->right = target;
			InsertSort(CSRight->left, CSRight);
			return;
		}
		else if (CS->right == NULL && CS->data > IS->left->data) {

			node*target = IS;
			node*tLeft = target->left;
			node*CSLeft = CS->left;
			node*CSRight = CS->right;
			tLeft->right = CS;
			target->left = CS;
			CS->left = tLeft;
			CS->right = target;
			CSLeft->right = NULL;
			InsertSort(IS, CS);
			printf("20133105 이재원\n");
			return;
		}
		else if (CS->data > IS->left->data) { 

			node*target = IS;
			node*tLeft = target->left;
			node*CSLeft = CS->left;
			node*CSRight = CS->right;
			tLeft->right = CS;
			target->left = CS;
			CS->left = tLeft;
			CS->right = target;
			CSLeft->right = CSRight;
			CSRight->left = CSLeft;

			InsertSort(CSLeft, CSRight);
		}
		else InsertSort(IS->left, CS);
	}
}
void RadixSort(int* data) {

	int bucket[10][4];
	int count[10];
	for (int i = 0; i < 10; i++) {
		for (int j = 0; j < 4; j++) {
			bucket[i][j] = NULL;
		}
		count[i] = 0;
	}
	printf("Path 1 >> \n");
	for (int i = 0; i < 8; i++) {
		switch (data[i] % 10) {
		case 0: bucket[0][count[0]] = data[i];
			count[0]++; break;
		case 1: bucket[1][count[1]] = data[i];
			count[1]++; break;
		case 2: bucket[2][count[2]] = data[i];
			count[2]++; break;
		case 3: bucket[3][count[3]] = data[i];
			count[3]++; break;
		case 4: bucket[4][count[4]] = data[i];
			count[4]++; break;
		case 5: bucket[5][count[5]] = data[i];
			count[5]++; break;
		case 6: bucket[6][count[6]] = data[i];
			count[6]++; break;
		case 7: bucket[7][count[7]] = data[i];
			count[7]++; break;
		case 8: bucket[8][count[8]] = data[i];
			count[8]++; break;
		case 9: bucket[9][count[9]] = data[i];
			count[9]++; break;
		}
	}
	int dataCount = 0;
	for (int i = 0; i < 10; i++) {
		printf("bucket %d :", i);
		for (int j = 0; j < 4; j++) {
			if (bucket[i][j] != NULL) {
				printf("%d ", bucket[i][j]);
				data[dataCount] = bucket[i][j];
				dataCount++;
			}
		}
		printf("\n");
	}
	printf("\n");
	printf("Path 2 >>\n");
	for (int i = 0; i < 8; i++)printf("%d ", data[i]);
	printf("\n");

	for (int i = 0; i < 10; i++) {
		for (int j = 0; j < 4; j++) {
			bucket[i][j] = NULL;
		}
		count[i] = 0;
	}
	printf("\nPath 3 >> \n");
	for (int i = 0; i < 8; i++) {
		switch (data[i] / 10) {
		case 0: bucket[0][count[0]] = data[i];
			count[0]++; break;
		case 1: bucket[1][count[1]] = data[i];
			count[1]++; break;
		case 2: bucket[2][count[2]] = data[i];
			count[2]++; break;
		case 3: bucket[3][count[3]] = data[i];
			count[3]++; break;
		case 4: bucket[4][count[4]] = data[i];
			count[4]++; break;
		case 5: bucket[5][count[5]] = data[i];
			count[5]++; break;
		case 6: bucket[6][count[6]] = data[i];
			count[6]++; break;
		case 7: bucket[7][count[7]] = data[i];
			count[7]++; break;
		case 8: bucket[8][count[8]] = data[i];
			count[8]++; break;
		case 9: bucket[9][count[9]] = data[i];
			count[9]++; break;
		}
	}
	dataCount = 0;
	for (int i = 0; i < 10; i++) {
		printf("bucket %d :", i);
		for (int j = 0; j < 4; j++) {
			if (bucket[i][j] != NULL) {
				printf("%d ", bucket[i][j]);
				data[dataCount] = bucket[i][j];
				dataCount++;
			}
		}
		printf("\n");
	}
	printf("\n");
	printf("Path 4 >>\n");
	for (int i = 0; i < 8; i++)printf("%d ", data[i]);
	printf("\nend 20133105 이재원 \n");

}
void LinearSearch(int* data, int num) {
	int i=0;
	while(1) {
		if (i > 7) {
			printf("Miss.. number ""%d"" is not on data\n", num);
			printf("\nend 20133105 이재원 \n");
			return;
		}
		else if (data[i] == num) {
			printf("Hit ! number ""%d"" is on data[%d]\n", num, i);
			printf("Address : %d\n", &data[i]);
			printf("\nend 20133105 이재원 \n");
			return;
		}
		else i++;
	}
}
void BinarySearch(int* data,int begin, int end, int num) {
	int middle = (begin + end) / 2;
	//printf("begin = %d , end = %d , middle = %d \n", begin, end, middle);
	if (begin > end) {
		printf("Miss.. number ""%d"" is not on data\n", num);
		printf("\nend 20133105 이재원 \n");
		return;
	}
	else if (data[middle] == num) {
		printf("Hit ! number ""%d"" is on data[%d]\n", num, middle);
		printf("Address : %d\n", &data[middle]);
		printf("\nend 20133105 이재원 \n");
		return;
	}
	else if (data[middle] > num) {
		BinarySearch(data, begin, middle - 1, num);
	}
	else if (data[middle] < num) {
		BinarySearch(data, middle + 1, end, num);
	}
}
int main() {
	int num = 0;
	int data[8] = { 69,10,30,2,16,8,31,22 }; //array
	// 2,10,16,30,69,8
	int* dataP = data;
	
	node* dataLink[8] = { NewNode(69),NewNode(10),NewNode(30),NewNode(2),NewNode(16),NewNode(8),NewNode(31),NewNode(22) }; //double linked list
	node* front = LinkingNode(dataLink);
	
	printf("Selection\n1.LinearSearch\n2.BinarySearch\n3.SelectionSort\n");
	printf("4.BubbleSort\n5.InsertSort\n6.RadixSort\n==================\n");
	printf("selection : ");
	scanf_s("%d", &num);
	switch (num) {
	case 1: LinearSearch(dataP, 22); break;
	case 2: BinarySearch(dataP, 0, 7, 100); break;
	case 3:	SelectionSort(dataP); break;
	case 4: BubbleSort(dataP); break;
	case 5: printf("Insert Sorting ! \n"); InsertSort(front, front->right); break;
	case 6: RadixSort(dataP); break;
	}
//	LinearSearch(dataP,22);
//	BinarySearch(dataP, 0, 7, 31);
//	SelectionSort(dataP);
//	BubbleSort(dataP);
//	printf("Insert Sorting ! \n");
//	InsertSort(front, front->right,front);
//	RadixSort(dataP);

	return 0;
}