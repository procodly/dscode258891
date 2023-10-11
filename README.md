-


-
-
--
-

--
-

-
-
--
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
--
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
--
-
-
-
-
-
-
-
-
-
-
-
--
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
--
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
--
-
-
-
-
-

--

--
-
-
-

-
-
-


































































# DS-CODES
#include<stdio.h>
#include<stdlib.h>

struct node
{
    int data;
    struct node* next;
};

struct node* head = NULL;

void insertionbeg(int item)
{
    struct node* temp = (struct node*)malloc(sizeof(struct node));
    temp->data = item;
    temp->next = head;
    head = temp;
}

void insertionend(int item)
{
    struct node* temp = (struct node*)malloc(sizeof(struct node));
    temp->data = item;
    temp->next = NULL;
    if (head == NULL)
    {
        head = temp;
        return;
    }
    struct node* ptr = head;
    while (ptr->next != NULL)
    {
        ptr = ptr->next;
    }
    ptr->next = temp;
}

void insertionanypos(int pos, int item)
{
    struct node* temp = (struct node*)malloc(sizeof(struct node));
    temp->data = item;
    temp->next = NULL;
    if (pos == 1)
    {
        temp->next = head;
        head = temp;
        return;
    }
    struct node* ptr = head;
    for (int i = 1; i < pos - 1 && ptr != NULL; i++)
    {
        ptr = ptr->next;
    }
    if (ptr == NULL)
    {
        printf("Invalid position\n");
    }
    else
    {
        temp->next = ptr->next;
        ptr->next = temp;
    }
}

void deletionbeg()
{
    if (head != NULL)
    {
        struct node* temp = head;
        head = head->next;
        free(temp);
    }
}

void deletionend()
{
    if (head == NULL)
    {
        printf("List is empty\n");
        return;
    }
    if (head->next == NULL)
    {
        free(head);
        head = NULL;
        return;
    }
    struct node* ptr = head;
    while (ptr->next->next != NULL)
    {
        ptr = ptr->next;
    }
    free(ptr->next);
    ptr->next = NULL;
}

void deletionanypos(int pos)
{
    if (head == NULL)
    {
        printf("List is empty\n");
        return;
    }
    struct node* temp = head;
    if (pos == 1)
    {
        head = head->next;
        free(temp);
        return;
    }
    for (int i = 1; i < pos - 1 && temp != NULL; i++)
    {
        temp = temp->next;
    }
    if (temp == NULL || temp->next == NULL)
    {
        printf("Invalid position\n");
    }
    else
    {
        struct node* delNode = temp->next;
        temp->next = temp->next->next;
        free(delNode);
    }
}

void printlinkedlist()
{
    struct node* ptr = head;
    while (ptr != NULL)
    {
        printf("%d\t", ptr->data);
        ptr = ptr->next;
    }
    printf("\n");
}

int main()
{
    int n, j, op, m, d;
    printf("Enter the number of nodes: ");
    scanf("%d", &n);

    printf("\nEnter the data of head: ");
    scanf("%d", &j);

    head = (struct node*)malloc(sizeof(struct node));
    head->data = j;
    head->next = NULL;

    struct node* ptr = head;
    for (int i = 2; i <= n; i++)
    {
        printf("Enter data of node %d: ", i);
        scanf("%d", &j);
        struct node* temp = (struct node*)malloc(sizeof(struct node));
        temp->data = j;
        temp->next = NULL;
        ptr->next = temp;
        ptr = temp;
    }

    printlinkedlist();

    do
    {
        printf("\nChoose:\n1. Insertion at beginning\n2. Insertion at end\n3. Insertion at any position\n4. Deletion at beginning\n5. Deletion at end\n6. Deletion at any position\n7. Exit\nEnter the option: ");
        scanf("%d", &op);

        switch (op)
        {
            case 1:
                printf("Enter the data to be inserted at the beginning: ");
                scanf("%d", &j);
                insertionbeg(j);
                printf("The list after insertion:\n");
                printlinkedlist();
                break;
            case 2:
                printf("Enter the data to be inserted at the end: ");
                scanf("%d", &j);
                insertionend(j);
                printf("The list after insertion:\n");
                printlinkedlist();
                break;
            case 3:
                printf("Enter the position: ");
                scanf("%d", &m);
                printf("Enter the data to be inserted at any position: ");
                scanf("%d", &d);
                insertionanypos(m, d);
                printf("The list after insertion:\n");
                printlinkedlist();
                break;
            case 4:
                printf("The list after deletion at the beginning:\n");
                deletionbeg();
                printlinkedlist();
                break;
            case 5:
                printf("The list after deletion at the end:\n");
                deletionend();
                printlinkedlist();
                break;
            case 6:
                printf("Enter the node to be deleted: ");
                scanf("%d", &j);
                deletionanypos(j);
                printf("The list after deletion:\n");
                printlinkedlist();
                break;
            case 7:
                exit(0);
                break;
            default:
                printf("Invalid option! Please try again.\n");
        }
    } while (1);

    return 0;
}

