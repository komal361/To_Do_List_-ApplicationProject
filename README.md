# To_Do_List_-Application_Project



import json
from datetime import datetime

def load_tasks():
    try:
        with open("tasks.json", "r") as file:
            tasks = json.load(file)
    except FileNotFoundError:
        tasks = []
    return tasks

def save_tasks(tasks):
    with open("tasks.json", "w") as file:
        json.dump(tasks, file)

def add_task(tasks):
    task_name = input("Enter task name: ")
    task_priority = input("Enter task priority (high/medium/low): ")
    due_date = input("Enter due date (YYYY-MM-DD): ")
    
    new_task = {
        "name": task_name,
        "priority": task_priority,
        "due_date": due_date,
        "completed": False
    }
    tasks.append(new_task)
    print("Task added successfully!")

def remove_task(tasks):
    task_index = int(input("Enter the task number to remove: "))
    if task_index >= 0 and task_index < len(tasks):
        del tasks[task_index]
        print("Task removed successfully!")
    else:
        print("Invalid task number.")

def mark_task_completed(tasks):
    task_index = int(input("Enter the task number to mark as completed: "))
    if task_index >= 0 and task_index < len(tasks):
        tasks[task_index]["completed"] = True
        print("Task marked as completed!")
    else:
        print("Invalid task number.")

def view_tasks(tasks):
    for index, task in enumerate(tasks):
        print(f"{index}. {task['name']} - Priority: {task['priority']} - Due Date: {task['due_date']} - Completed: {task['completed']}")

def main():
    tasks = load_tasks()

    while True:
        print("\n1. Add Task\n2. Remove Task\n3. Mark Task as Completed\n4. View Tasks\n5. Exit")
        choice = input("Enter your choice: ")

        if choice == "1":
            add_task(tasks)
        elif choice == "2":
            remove_task(tasks)
        elif choice == "3":
            mark_task_completed(tasks)
        elif choice == "4":
            view_tasks(tasks)
        elif choice == "5":
            save_tasks(tasks)
            print("Exiting the program.")
            break

if __name__ == "__main__":
    main()
