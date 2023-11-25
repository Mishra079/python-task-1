# python-task-1
A To-do list application
import os

def display_menu():
    print("\nCommand Menu:")
    print("1. Show To-Do List")
    print("2. Add Task")
    print("3. Update Task")
    print("4. Remove Task")
    print("5. Exit")

def show_todo_list():
    if os.path.exists("todo.txt"):
        with open("todo.txt", "r") as file:
            tasks = file.readlines()
            if tasks:
                print("\nTo-Do List:")
                for i, task in enumerate(tasks, start=1):
                    print(f"{i}. {task.strip()}")
            else:
                print("\nTo-Do List is empty.")
    else:
        print("\nTo-Do List does not exist. Create a new task to start.")

def add_task():
    task = input("Enter the task: ")
    with open("todo.txt", "a") as file:
        file.write(task + "\n")
    print(f"Task '{task}' added to the To-Do List.")

def update_task():
    show_todo_list()
    task_number = int(input("Enter the task number to update: "))
    new_task = input("Enter the updated task: ")

    with open("todo.txt", "r") as file:
        tasks = file.readlines()

    if 1 <= task_number <= len(tasks):
        tasks[task_number - 1] = new_task + "\n"

        with open("todo.txt", "w") as file:
            file.writelines(tasks)

        print(f"Task {task_number} updated.")
    else:
        print("Invalid task number.")

def remove_task():
    show_todo_list()
    task_number = int(input("Enter the task number to remove: "))

    with open("todo.txt", "r") as file:
        tasks = file.readlines()

    if 1 <= task_number <= len(tasks):
        removed_task = tasks.pop(task_number - 1)

        with open("todo.txt", "w") as file:
            file.writelines(tasks)

        print(f"Task removed: {removed_task.strip()}")
    else:
        print("Invalid task number.")

def main():
    while True:
        display_menu()
        choice = input("\nEnter your choice (1-5): ")

        if choice == "1":
            show_todo_list()
        elif choice == "2":
            add_task()
        elif choice == "3":
            update_task()
        elif choice == "4":
            remove_task()
        elif choice == "5":
            print("Exiting the To-Do List application. Goodbye!")
            break
        else:
            print("Invalid choice. Please enter a number between 1 and 5.")

if __name__ == "__main__":
    main()

