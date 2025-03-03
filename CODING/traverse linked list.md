Here are the solutions to the three problems in C++: **Third-smallest element in an array**, **Linked List Traversal to reach a particular node**, and **Nth element from the end of a linked list**. I'll provide **brute-force**, **better**, and **optimal** approaches for each problem.

---

### **1. Third-Smallest Element in an Array**

#### **Brute Force Approach**
- Sort the array and return the third element.
- **Time Complexity**: O(n log n) due to sorting.
- **Space Complexity**: O(1) if sorting is done in-place.

```cpp
#include <iostream>
#include <algorithm>
#include <vector>
using namespace std;

int thirdSmallestBrute(vector<int>& arr) {
    if (arr.size() < 3) {
        cout << "Array has less than 3 elements." << endl;
        return -1;
    }
    sort(arr.begin(), arr.end());
    return arr[2];
}

int main() {
    vector<int> arr = {12, 3, 5, 7, 19};
    cout << "Third smallest (Brute): " << thirdSmallestBrute(arr) << endl;
    return 0;
}
```

---

#### **Better Approach**
- Use a min-heap (priority queue) to find the third smallest element.
- **Time Complexity**: O(n + k log n), where `k = 3`.
- **Space Complexity**: O(n) for the heap.

```cpp
#include <iostream>
#include <queue>
#include <vector>
using namespace std;

int thirdSmallestBetter(vector<int>& arr) {
    if (arr.size() < 3) {
        cout << "Array has less than 3 elements." << endl;
        return -1;
    }
    priority_queue<int, vector<int>, greater<int>> minHeap(arr.begin(), arr.end());
    for (int i = 0; i < 2; i++) {
        minHeap.pop();
    }
    return minHeap.top();
}

int main() {
    vector<int> arr = {12, 3, 5, 7, 19};
    cout << "Third smallest (Better): " << thirdSmallestBetter(arr) << endl;
    return 0;
}
```

---

#### **Optimal Approach**
- Use a modified version of Quickselect (similar to QuickSort) to find the third smallest element.
- **Time Complexity**: O(n) on average.
- **Space Complexity**: O(1).

```cpp
#include <iostream>
#include <vector>
#include <climits>
using namespace std;

int partition(vector<int>& arr, int low, int high) {
    int pivot = arr[high];
    int i = low - 1;
    for (int j = low; j < high; j++) {
        if (arr[j] < pivot) {
            i++;
            swap(arr[i], arr[j]);
        }
    }
    swap(arr[i + 1], arr[high]);
    return i + 1;
}

int quickSelect(vector<int>& arr, int low, int high, int k) {
    if (low <= high) {
        int pi = partition(arr, low, high);
        if (pi == k - 1) {
            return arr[pi];
        } else if (pi > k - 1) {
            return quickSelect(arr, low, pi - 1, k);
        } else {
            return quickSelect(arr, pi + 1, high, k);
        }
    }
    return INT_MAX;
}

int thirdSmallestOptimal(vector<int>& arr) {
    if (arr.size() < 3) {
        cout << "Array has less than 3 elements." << endl;
        return -1;
    }
    return quickSelect(arr, 0, arr.size() - 1, 3);
}

int main() {
    vector<int> arr = {12, 3, 5, 7, 19};
    cout << "Third smallest (Optimal): " << thirdSmallestOptimal(arr) << endl;
    return 0;
}
```

---

### **2. Linked List Traversal to Reach a Particular Node**

#### **Brute Force Approach**
- Traverse the linked list until the desired node is found.
- **Time Complexity**: O(n).
- **Space Complexity**: O(1).

```cpp
#include <iostream>
using namespace std;

struct Node {
    int data;
    Node* next;
    Node(int val) : data(val), next(nullptr) {}
};

Node* traverseToNodeBrute(Node* head, int target) {
    Node* current = head;
    while (current != nullptr) {
        if (current->data == target) {
            return current;
        }
        current = current->next;
    }
    return nullptr;
}

int main() {
    Node* head = new Node(1);
    head->next = new Node(2);
    head->next->next = new Node(3);
    head->next->next->next = new Node(4);

    int target = 3;
    Node* result = traverseToNodeBrute(head, target);
    if (result) {
        cout << "Node found: " << result->data << endl;
    } else {
        cout << "Node not found." << endl;
    }
    return 0;
}
```

---

### **3. Nth Element from the End of a Linked List**

#### **Brute Force Approach**
- Traverse the list to find its length, then traverse again to the (length - n)th node.
- **Time Complexity**: O(2n) = O(n).
- **Space Complexity**: O(1).

```cpp
#include <iostream>
using namespace std;

struct Node {
    int data;
    Node* next;
    Node(int val) : data(val), next(nullptr) {}
};

Node* nthFromEndBrute(Node* head, int n) {
    int length = 0;
    Node* current = head;
    while (current != nullptr) {
        length++;
        current = current->next;
    }
    if (n > length) {
        return nullptr;
    }
    current = head;
    for (int i = 0; i < length - n; i++) {
        current = current->next;
    }
    return current;
}

int main() {
    Node* head = new Node(1);
    head->next = new Node(2);
    head->next->next = new Node(3);
    head->next->next->next = new Node(4);

    int n = 2;
    Node* result = nthFromEndBrute(head, n);
    if (result) {
        cout << "Nth node from end: " << result->data << endl;
    } else {
        cout << "Invalid position." << endl;
    }
    return 0;
}
```

---

#### **Optimal Approach (Two-Pointer Technique)**
- Use two pointers: one starts at the head, and the other starts after `n` steps. Move both pointers until the second pointer reaches the end.
- **Time Complexity**: O(n).
- **Space Complexity**: O(1).

```cpp
#include <iostream>
using namespace std;

struct Node {
    int data;
    Node* next;
    Node(int val) : data(val), next(nullptr) {}
};

Node* nthFromEndOptimal(Node* head, int n) {
    Node* first = head;
    Node* second = head;
    for (int i = 0; i < n; i++) {
        if (second == nullptr) {
            return nullptr; // Invalid position
        }
        second = second->next;
    }
    while (second != nullptr) {
        first = first->next;
        second = second->next;
    }
    return first;
}

int main() {
    Node* head = new Node(1);
    head->next = new Node(2);
    head->next->next = new Node(3);
    head->next->next->next = new Node(4);

    int n = 2;
    Node* result = nthFromEndOptimal(head, n);
    if (result) {
        cout << "Nth node from end: " << result->data << endl;
    } else {
        cout << "Invalid position." << endl;
    }
    return 0;
}
```

---

### **Summary**
- **Third-Smallest Element**: Brute (sorting), Better (min-heap), Optimal (Quickselect).
- **Linked List Traversal**: Brute (linear traversal).
- **Nth Element from End**: Brute (two traversals), Optimal (two-pointer technique).
