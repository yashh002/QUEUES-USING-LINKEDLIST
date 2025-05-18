# QUEUE USING LINKEDLIST
#include<stdio.h>
#include<stdlib.h>
struct node {
    int data;
    struct node *next;
};
struct node *rear = NULL, *front = NULL, *newnode, *temp;

void enqueue(int value) {
    newnode = malloc(sizeof(struct node));
    if (newnode == NULL) {
        printf("Memory allocation failed\n");
        return;
    }
    newnode->data = value;
    newnode->next = NULL;

    if (rear == NULL && front == NULL) {
        front = rear = newnode;
    } else {
        rear->next = newnode;
        rear = newnode;
    }
}
void dequeue() {
    if (front == NULL) {
        printf("Queue is empty\n");
    } else {
        temp = front;
        front = front->next;
        printf("Dequeued: %d\n", temp->data);
        free(temp);
        if (front == NULL) {
            rear = NULL; 
        }
    }
}
void display() {
    if (front == NULL) {
        printf("Queue is empty\n");
        return;
    }

    temp = front;
    printf("Queue elements: ");
    while (temp != NULL) {
        printf("%d -> ", temp->data);
        temp = temp->next;
    }
    printf("NULL\n");
}
int main() {
    int choice, value;
    while (1) {
        printf("\nMenu:\n 1. Enqueue\n 2. Dequeue\n 3. Display\n 4. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch (choice) {
            case 1:
                printf("Enter value to enqueue: ");
                scanf("%d", &value);
                enqueue(value);  // Pass value to enqueue
                break;
            case 2:
                dequeue();
                break;
            case 3:
                display();
                break;
            case 4:
                exit(0);
            default:
                printf("Invalid choice\n");
        }
    }
    return 0;
}
