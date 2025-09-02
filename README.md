# Laboratory_12

Tasks:

->Handling Btree


# Memo: Binary Trees in C



## 1. What is a Binary Tree?

- A **binary tree** is a hierarchical data structure.
- Each node contains:
  - **Data**
  - **Pointer to the left child**
  - **Pointer to the right child**
- The top node is the **root**.
- A node with no children is a **leaf**.

---

## 2. Defining a Node

```c
typedef struct Node {
    int data;
    struct Node *left; //why struct needed here??
    struct Node *right;
} Node;
```

---

## 3. Creating a New Node

```c
Node* createNode(int value) {
    Node* newNode = malloc(sizeof(Node));
    if (newNode == NULL) {
        printf("Memory allocation failed\n");
        exit(1);
    }
    newNode->data = value;
    newNode->left = NULL;
    newNode->right = NULL;
    return newNode;
}
```

---

## 4. Insertion (Binary Search Tree Example)

```c
Node* insert(Node* root, int value) {
    if (root == NULL) return createNode(value);

    if (value < root->data)
        root->left = insert(root->left, value);
    else if (value > root->data)
        root->right = insert(root->right, value);

    return root;
}
```

---

## 5. Traversal Methods

### Inorder (Left → Root → Right)
```c
void inorder(Node* root) {
    if (root != NULL) {
        inorder(root->left);
        printf("%d ", root->data);
        inorder(root->right);
    }
}
```

### Preorder (Root → Left → Right)
```c
void preorder(Node* root) {
    if (root != NULL) {
        printf("%d ", root->data);
        preorder(root->left);
        preorder(root->right);
    }
}
```

### Postorder (Left → Right → Root)
```c
void postorder(Node* root) {
    if (root != NULL) {
        postorder(root->left);
        postorder(root->right);
        printf("%d ", root->data);
    }
}
```

---

## 6. Searching in a Binary Search Tree

```c
Node* search(Node* root, int value) {
    if (root == NULL || root->data == value)
        return root;
    if (value < root->data)
        return search(root->left, value);
    else
        return search(root->right, value);
}
```

---

## 7. Deleting the Tree (Freeing Memory)

```c
void deleteTree(Node* root) {
    if (root == NULL) return;
    deleteTree(root->left);
    deleteTree(root->right);
    free(root);
}
```

---

## 8. Advantages and Disadvantages

**Advantages:**
- Hierarchical structure for efficient searching and sorting.
- Dynamic size (nodes allocated as needed).
- Useful for many algorithms (search trees, heaps, expression trees).

**Disadvantages:**
- More memory (extra pointers per node).
- Complex implementation compared to arrays or linked lists.
- Performance depends on tree balance (unbalanced tree ≈ linked list).

---

## 9. Use Cases

- Binary Search Trees (BST) for fast lookup.
- Expression trees in compilers, calculator?

