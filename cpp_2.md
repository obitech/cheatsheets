### 1. Lists
#### 1.1 Single Linked List
#### Insert front
```c++
void insert_front(lelem *&head, int d) {
    lelem *start = new lelem;
    start->data = d;
    start->next = head;
    head = start;
}
```

#### Insert back
```c++
void insert_back(lelem *&head, int d){ 
    lelem *item = new lelem;
    item->data = d
    item->next = NULL;

    if (head) {
        lelem *lptr = head;  
        while(lptr->next)
            lptr = lptr->next;
        lptr->next = back;          
    else
        head = back;
}
```

#### Insert sorted
```c++
void insert_sorted(lelem *&head, int d) {
    if (!head || d < head->data)
        insert_front(head,d);
    else
        insert_front(head->next, d);
}
```

#### Remove back
```c++
void remove_back(lelem *&head) {
    if (!head)
        return;

    // 1 element
    if (!head->next) {
        delete head;
        head = NULL;
        return;
    }
    
    lelem *tmp = head;
    while(tmp->next->next)
        tmp = tmp->next;

    delete tmp->next;
    tmp->next = NULL;
    return;
}
```
#### Remove data
```c++
void remove_data(lelem *&head, int val) {
    if (!head)
        return
    if (head->data == val) {
        remove_front(head);
        return
    }
    remove_data(head->next, val);
}
```
#### Copy
```c++
void copy(lelem* head1, lelem* &head2) {
    head2 = NULL;

    if (head1 == NULL)
        return;
    
    insert_front(head2,head1->data);
    
    lelem* tmp = head1->next;

    lelem* tail = head2;
    
    while (tmp != NULL) {
        lelem* newelem = new lelem;
        newelem->data = tmp->data;
        newelem->next = NULL;
        tail->next = newelem;
        
        tmp = tmp->next;

        tail = tail->next;
    }
}

```
#### 1.2 Double Linked List
#### Insert at
```c++
void DList::insert_at(int pos, int d) {
    // 0 elements
    if (head == NULL || pos == 0)
        insert_front(d);
    else {
        // Pos bigger than list
        if (pos >= size)
            insert_back(d);
        else {
            dlelem *tmp = head;
            for (int i = 0; i < pos; i++)
                tmp = tmp->next;
            dlelem *item = new dlelem;
            item->data = d;
            item->prev = tmp;
            item->next = tmp->next;
            tmp->next = item;
            item->next->prev = item;
            size++;
        }
    }
}
```
#### Remove data
```c++
bool DList::remove_data(int d) {
    if (!head) 
        return false;

    dlelem *tmp = head;

    // Search for d
    while (tmp && tmp->data != d)
        tmp = tmp->next;

    // d not found
    if (!tmp)
        return false;

    // d is first element
    if (tmp == head) {
        // 1 element in list
        if (head == tail) {
            delete head;
            head = tail = NULL;
            size = 0;
            return true;
        }
        // More elements
        head = head->next;
        head->prev = NULL;
        delete tmp;
        size--;
        return true;
    }

    // d is last element
    if (tmp == tail) {
        tail = tmp->prev;
        tail->next = NULL;
        delete tmp;
        size--;
        return true;
    }

    // d is somewhere in the middle
    tmp->prev->next = tmp->next;
    tmp->next->prev = tmp->prev;
    delete tmp;
    size--;
    return true;
}
```

### 2. OOP
#### Class definition
```c++
class Test {
    private:
        int a;
        int b;
    public:
        Test();
        ~Test();
        bool exists();
};

Test::Test() {
    a = b = 0;
}

Test::~Test() {
    // Remove everything which was dynamically allocated
}

bool Test::exists() {
    return true;
}
```
#### Operator overload
```c++
class Number {
    private:
        int val;
    public:
        Number();
        int operator+(Number);
        friend ostream& operator<<(ostream &, Number);
};

int Number::operator+(Number x) {
    return val + x.val;
}

ostream& operator<<(ostream& os, Number x) {
    os << "Our number is " << x.val << endl;
    return os;
}
```

### 3. Dynamic Memory
#### 2D Matrix
```c++
// Create and set 0
m = new int*[rows];
for (int i = 0; i < rows; i++) {
    m[i] = new int[cols];
    
    for (int j = 0; j < i; j++) {
        m[i][j] = 0
    }
}

// Delete
for (int i = 0; i < rows; i++)
    delete[] m[i];
delete[] m;
```