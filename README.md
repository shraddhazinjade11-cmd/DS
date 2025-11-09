Queue
class CallCenterQueue:
    def __init__(self):
        self.queue = []   # Initialize an empty list to store calls

    def addCall(self, customerID, callTime):
        """Add a call with customer ID and call time to the queue"""
        call = {"CustomerID": customerID, "CallTime": callTime}
        self.queue.append(call)
        print(f"Call from Customer {customerID} added at {callTime} minutes.")

    def answerCall(self):
        """Answer and remove the first call in the queue"""
        if not self.isQueueEmpty():
            call = self.queue.pop(0)
            print(f"Answered call from Customer {call['CustomerID']} (Call time: {call['CallTime']} mins).")
        else:
            print("No calls in the queue to answer!")

    def viewQueue(self):
        """View all calls currently in the queue"""
        if not self.isQueueEmpty():
            print("\nCurrent Call Queue:")
            for i, call in enumerate(self.queue, start=1):
                print(f"{i}. Customer ID: {call['CustomerID']}, Call Time: {call['CallTime']} mins")
        else:
            print("The call queue is empty.")

    def isQueueEmpty(self):
        """Check if the queue is empty"""
        return len(self.queue) == 0


# ---- Simulation with user input ----
call_center = CallCenterQueue()

while True:
    print("\n--- Call Center Menu ---")
    print("1. Add Call")
    print("2. Answer Call")
    print("3. View Queue")
    print("4. Check if Queue is Empty")
    print("5. Exit")

    choice = input("Enter your choice (1-5): ")

    if choice == "1":
        customerID = input("Enter Customer ID: ")
        callTime = input("Enter Call Time (in minutes): ")
        call_center.addCall(customerID, callTime)

    elif choice == "2":
        call_center.answerCall()

    elif choice == "3":
        call_center.viewQueue()

    elif choice == "4":
        if call_center.isQueueEmpty():
            print("The call queue is empty.")
        else:
            print("The call queue is not empty.")

    elif choice == "5":
        print("Exiting Call Center Simulation. Goodbye!")
        break

    else:
        print("Invalid choice. Please enter a number between 1 and 5.")




Link list
Q4. Student Record Management using Singly Linked List
class
class Node:
    def _init_(self, roll, name, marks):
        self.roll = roll
        self.name = name
        self.marks = marks
        self.next = None


class StudentList:
    def _init_(self):
        self.head = None

    def addStudent(self, roll, name, marks):
        new_node = Node(roll, name, marks)
        if not self.head:
            self.head = new_node
        else:
            temp = self.head
            while temp.next:
                temp = temp.next
            temp.next = new_node
        print("Student added successfully.")

    def display(self):
        if not self.head:
            print("No records to display.")
            return
        temp = self.head
        while temp:
            print(f"Roll: {temp.roll}, Name: {temp.name}, Marks: {temp.marks}")
            temp = temp.next

    def search(self, roll):
        temp = self.head
        while temp:
            if temp.roll == roll:
                print(f"Found: Roll {temp.roll}, Name {temp.name}, Marks {temp.marks}")
                return
            temp = temp.next
        print("Student not found.")

    def delete(self, roll):
        temp = self.head
        if temp is None:
            print("No record found.")
            return
        if temp.roll == roll:
            self.head = temp.next
            print("Record deleted.")
            return
        while temp.next:
            if temp.next.roll == roll:
                temp.next = temp.next.next
                print("Record deleted.")
                return
            temp = temp.next
        print("Record not found.")


# Example
s = StudentList()
s.addStudent(1, "Alice", 85)
s.addStudent(2, "Bob", 90)
s.display()
s.search(2)
s.delete(1)
s.display()


BST
Q8. Binary Search Tree (BST)
class Node:
    def _init_(self, key):
        self.key = key
        self.left = None
        self.right = None


class BST:
    def _init_(self):
        self.root = None

    def insert(self, root, key):
        if root is None:
            return Node(key)
        if key < root.key:
            root.left = self.insert(root.left, key)
        else:
            root.right = self.insert(root.right, key)
        return root

    def inorder(self, root):
        if root:
            self.inorder(root.left)
            print(root.key, end=" ")
            self.inorder(root.right)

    def search(self, root, key):
        if root is None or root.key == key:
            return root
        if key < root.key:
            return self.search(root.left, key)
        return self.search(root.right, key)

    def delete(self, root, key):
        if root is None:
            return root
        if key < root.key:
            root.left = self.delete(root.left, key)
        elif key > root.key:
            root.right = self.delete(root.right, key)
        else:
            if root.left is None:
                return root.right
            elif root.right is None:
                return root.left
            temp = self.minValueNode(root.right)
            root.key = temp.key
            root.right = self.delete(root.right, temp.key)
        return root

    def minValueNode(self, node):
        current = node
        while current.left is not None:
            current = current.left
        return current


# Example
tree = BST()
root = None
for key in [50, 30, 70, 20, 40, 60, 80]:
    root = tree.insert(root, key)

print("Inorder traversal:")
tree.inorder(root)

print("\nSearch 40:", "Found" if tree.search(root, 40) else "Not Found")

print("\nDelete 20")
root = tree.delete(root, 20)
tree.inorder(root)

selection and bubble sort
# Employee salaries list
salaries = [45000.0, 52000.5, 30000.0, 75000.2, 61000.7, 48000.9, 90000.4]

# --- Selection Sort ---
def selection_sort(arr):
    for i in range(len(arr)):
        min_idx = i
        for j in range(i + 1, len(arr)):
            if arr[j] < arr[min_idx]:
                min_idx = j
        arr[i], arr[min_idx] = arr[min_idx], arr[i]

# --- Bubble Sort ---
def bubble_sort(arr):
    n = len(arr)
    for i in range(n - 1):
        for j in range(n - 1 - i):
            if arr[j] > arr[j + 1]:
                arr[j], arr[j + 1] = arr[j + 1], arr[j]

# Using Selection Sort
sel_salaries = salaries.copy()
selection_sort(sel_salaries)
print("Top 5 salaries (Selection Sort):", sel_salaries[-5:][::-1])

# Using Bubble Sort
bub_salaries = salaries.copy()
bubble_sort(bub_salaries)
print("Top 5 salaries (Bubble Sort):", bub_salaries[-5:][::-1])

