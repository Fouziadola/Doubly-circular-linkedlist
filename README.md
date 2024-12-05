# Doubly-circular-linkedlist
#include <iostream>
using namespace std;

class Node {
public:
    int data;
    Node* prev;
    Node* next;
};

Node* insert_atfirst(Node* head, int value) {
    Node* newNode1 = new Node();
    newNode1->data = value;
    newNode1->prev = head->prev; 
    newNode1->next = head;       
    head->prev->next = newNode1;  
    head->prev = newNode1;        
    return newNode1;             
}

Node* insert_atlast(Node* head, int value) {
    Node* newNode2 = new Node();
    newNode2->data = value;
    if (!head) {
        newNode2->next = newNode2->prev = newNode2;
        return newNode2; 
    }
    Node* last = head->prev;
    newNode2->next = head;
    newNode2->prev = last;
    last->next = newNode2;
    head->prev = newNode2;
    return head;
}
Node* insert_before(Node* head,int value,int target){
     Node* temp = head;
    Node* newNode3 = new Node();
    while (temp->next->data != target)
    {
        temp = temp->next;
    }
    newNode3->data = value;
    newNode3->prev = temp;
    newNode3->next = temp->next;
    temp->next->prev = newNode3;
    temp->next = newNode3;
    return head;
   
}
Node* insert_after(Node *head, int value, int target)
{
    Node *temp = head;
    while (temp->data != target)
    {
        temp = temp->next;
    }

    Node *newNode4 = new Node();
    newNode4->data = value;

    newNode4->next = temp->next;
    newNode4->prev = temp;

    temp->next->prev = newNode4;
    temp->next = newNode4;
    return head;
}

Node* insert_index(Node *head, int value, int index)
{
    Node* neww= head;
    if (index == 0)
    {
        Node *newNode5 = new Node();
        newNode5->data = value;
        newNode5->prev =neww;
        newNode5->next = head;
        head->prev = newNode5;
        neww->next = newNode5;
        head = newNode5;
    }
    else
    {
        int currentIndex = 1;
        Node *temp = head->next;
        while (true)
        {
            if (temp == head)
            {
                break;
            }
            if (currentIndex == index)
            {
                break;
            }
            else
            {
                temp = temp->next;
                currentIndex++;
            }
        }

        Node *newNode = new Node();
        newNode->data = value;

        newNode->prev = temp->prev;
        newNode->next = temp;

        temp->prev->next = newNode;
        temp->prev = newNode;
    }
    return head;
}
void print(Node** head){
    Node* Cursor = *head;
    do {
        cout << Cursor->data << " ";
        Cursor = Cursor->next;
    } while (Cursor != *head);
}
int main() {
    Node* head = new Node();
    head->data = 10;
    head->next = head;
    head->prev = head;

    head = insert_atfirst(head, 5);
    head = insert_atlast(head, 15);
    head=insert_before(head,12,15);
    head= insert_after(head,20,15);
    head=insert_index(head,13,3);
    print(&head);

    return 0;
}
