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

