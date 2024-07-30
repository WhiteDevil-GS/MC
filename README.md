prg-1
#include <stdio.h>

typedef struct {
    int src, dest, weight;
} Edge;

#define NUM_VERTICES 7
#define NUM_EDGES 9

Edge edges[] = {
    {0, 0, 0},
    {6, 1, 10}, {2, 1, 28}, {3, 2, 16},
    {7, 2, 14}, {4, 3, 12}, {5, 4, 22},
    {6, 5, 25}, {7, 5, 24}, {7, 4, 18}
};

void adjust(Edge a[], int i, int n);
void buildMinHeap(Edge a[], int n);
Edge deleteMin(Edge a[], int* n);

int parent[NUM_VERTICES + 1];
void simpleUnion(int i, int j);
int simpleFind(int i);

void kruskalMST(Edge edges[], int numEdges) {
    for (int i = 1; i <= NUM_VERTICES; i++) {
        parent[i] = -1;
    }

    Edge t[NUM_VERTICES + 1];
    int minCost = 0;
    int i = 0;

    buildMinHeap(edges, numEdges);

    while (i < NUM_VERTICES - 1 && numEdges > 0) {
        Edge minEdge = deleteMin(edges, &numEdges);
        int j = simpleFind(minEdge.src);
        int k = simpleFind(minEdge.dest);
        if (j != k) {
            i++;
            t[i] = minEdge;
            minCost += minEdge.weight;
            simpleUnion(j, k);
        }
    }

    if (i != NUM_VERTICES - 1) {
        printf("No spanning tree exists.\n");
        return;
    }

    printf("Edges in the minimum spanning tree:\n");
    for (int j = 1; j <= NUM_VERTICES - 1; j++) {
        printf("(%d, %d) : %d\n", t[j].src, t[j].dest, t[j].weight);
    }
    printf("Minimum cost: %d\n", minCost);
}

int main() {
    printf("Edges before sorting:\n");
    for (int i = 1; i <= NUM_EDGES; i++) {
        printf("(%d, %d) : %d\n", edges[i].src, edges[i].dest, edges[i].weight);
    }

    kruskalMST(edges, NUM_EDGES);
    return 0;
}

void buildMinHeap(Edge a[], int n) {
    for (int i = n / 2; i >= 1; i--) {
        adjust(a, i, n);
    }
}

void adjust(Edge a[], int i, int n) {
    int j = 2 * i;
    Edge item = a[i];
    while (j <= n) {
        if (j < n && a[j].weight > a[j + 1].weight) {
            j++;
        }
        if (item.weight <= a[j].weight) {
            break;
        }
        a[j / 2] = a[j];
        j *= 2;
    }
    a[j / 2] = item;
}

Edge deleteMin(Edge a[], int* n) {
    Edge min = a[1];
    a[1] = a[*n];
    (*n)--;
    adjust(a, 1, *n);
    return min;
}

void simpleUnion(int i, int j) {
    parent[i] = j;
}

int simpleFind(int i) {
    while (parent[i] >= 0) {
        i = parent[i];
    }
    return i;
}
