# Ai
advance jarves
<br>
#include <stdio.h>
#include <stdlib.h>

#define MAX_SIZE 100

struct Deque {
    int arr[MAX_SIZE];
    int front, rear;
};

void initialize(struct Deque* dq) {
    dq->front = -1;
    dq->rear = -1;
}

int isFull(struct Deque* dq) {
    return (dq->front == 0 && dq->rear == MAX_SIZE - 1) || (dq->front == dq->rear + 1);
}

int isEmpty(struct Deque* dq) {
    return dq->front == -1;
}

void insertFront(struct Deque* dq, int data) {
    if (isFull(dq)) {
        printf("Queue is full, cannot insert at the front.\n");
        return;
    }

    if (dq->front == -1) {
        dq->front = dq->rear = 0;
    } else if (dq->front == 0) {
        dq->front = MAX_SIZE - 1;
    } else {
        dq->front--;
    }

    dq->arr[dq->front] = data;
}

void insertRear(struct Deque* dq, int data) {
    if (isFull(dq)) {
        printf("Queue is full, cannot insert at the rear.\n");
        return;
    }

    if (dq->front == -1) {
        dq->front = dq->rear = 0;
    } else if (dq->rear == MAX_SIZE - 1) {
        dq->rear = 0;
    } else {
        dq->rear++;
    }

    dq->arr[dq->rear] = data;
}

int deleteFront(struct Deque* dq) {
    if (isEmpty(dq)) {
        printf("Queue is empty, cannot delete from the front.\n");
        return -1;
    }

    int data = dq->arr[dq->front];

    if (dq->front == dq->rear) {
        dq->front = dq->rear = -1;
    } else if (dq->front == MAX_SIZE - 1) {
        dq->front = 0;
    } else {
        dq->front++;
    }

    return data;
}

int deleteRear(struct Deque* dq) {
    if (isEmpty(dq)) {
        printf("Queue is empty, cannot delete from the rear.\n");
        return -1;
    }

    int data = dq->arr[dq->rear];

    if (dq->front == dq->rear) {
        dq->front = dq->rear = -1;
    } else if (dq->rear == 0) {
        dq->rear = MAX_SIZE - 1;
    } else {
        dq->rear--;
    }

    return data;
}

int getFront(struct Deque* dq) {
    if (isEmpty(dq)) {
        printf("Queue is empty, no front element.\n");
        return -1;
    }
    return dq->arr[dq->front];
}

int getRear(struct Deque* dq) {
    if (isEmpty(dq)) {
        printf("Queue is empty, no rear element.\n");
        return -1;
    }
    return dq->arr[dq->rear];
}

int main() {
    struct Deque dq;
    initialize(&dq);

    insertFront(&dq, 1);
    insertRear(&dq, 2);
    insertFront(&dq, 3);

    printf("Front element: %d\n", getFront(&dq));
    printf("Rear element: %d\n", getRear(&dq));

    deleteFront(&dq);

    printf("Front element after deletion: %d\n", getFront(&dq));

    return 0;
}
