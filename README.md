# TaskManager
Task Manager using Queues and Stacks

# Code
from collections import deque

class TaskManager:
    def __init__(self):
        self.task_queue = deque()  # Queue for tasks
        self.undo_stack = []  # Stack for undoing completed tasks

    def add_task(self, task):
        self.task_queue.append(task)
        print(f'Task "{task}" added.')

    def complete_task(self):
        if self.task_queue:
            completed_task = self.task_queue.popleft()
            self.undo_stack.append(completed_task)
            print(f'Task "{completed_task}" completed.')
        else:
            print("No tasks to complete.")

    def undo_last_task(self):
        if self.undo_stack:
            last_task = self.undo_stack.pop()
            self.task_queue.appendleft(last_task)
            print(f'Task "{last_task}" undone and added back to queue.')
        else:
            print("No task to undo.")

    def view_tasks(self):
        if self.task_queue:
            print("Current tasks:", list(self.task_queue))
        else:
            print("No pending tasks.")

if __name__ == "__main__":
    manager = TaskManager()
    while True:
        print("\nOptions: add, complete, undo, view, exit")
        choice = input("Choose an option: ").strip().lower()
        if choice == "add":
            task = input("Enter task: ")
            manager.add_task(task)
        elif choice == "complete":
            manager.complete_task()
        elif choice == "undo":
            manager.undo_last_task()
        elif choice == "view":
            manager.view_tasks()
        elif choice == "exit":
            print("Exiting Task Manager.")
            break
        else:
            print("Invalid option, try again.")
