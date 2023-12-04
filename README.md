```python
import os

def display_menu():
    print("Menu:")
    print("1. List files and directories in a directory")
    print("2. Create a directory")
    print("3. Delete a file or directory")
    print("4. Rename a file or directory")
    print("5. Read the contents of a file")
    print("6. Write to a file")
    print("7. Exit")

def list_files_and_directories(directory):
    try:
        items = os.listdir(directory)
        for item in items:
            print(item)
    except FileNotFoundError:
        print(f"Directory '{directory}' not found.")
    except PermissionError:
        print(f"Permission denied for directory '{directory}'.")

def create_directory(directory):
    try:
        os.mkdir(directory)
        print(f"Directory '{directory}' created successfully.")
    except FileExistsError:
        print(f"Directory '{directory}' already exists.")
    except PermissionError:
        print(f"Permission denied for creating directory '{directory}'.")

def delete_file_or_directory(path):
    try:
        if os.path.isfile(path):
            os.remove(path)
            print(f"File '{path}' deleted successfully.")
        elif os.path.isdir(path):
            os.rmdir(path)
            print(f"Directory '{path}' deleted successfully.")
    except FileNotFoundError:
        print(f"File or directory '{path}' not found.")
    except PermissionError:
        print(f"Permission denied for deleting '{path}'.")

def rename_file_or_directory(src, dest):
    try:
        os.rename(src, dest)
        print(f"Renamed '{src}' to '{dest}' successfully.")
    except FileNotFoundError:
        print(f"File or directory '{src}' not found.")
    except PermissionError:
        print(f"Permission denied for renaming '{src}'.")

def read_file_contents(file_path):
    try:
        with open(file_path, "r") as file:
            contents = file.read()
            print(f"Contents of '{file_path}':")
            print(contents)
    except FileNotFoundError:
        print(f"File '{file_path}' not found.")
    except PermissionError:
        print(f"Permission denied for reading '{file_path}'.")

def write_to_file(file_path, data):
    try:
        with open(file_path, "w") as file:
            file.write(data)
        print(f"Data written to '{file_path}' successfully.")
    except PermissionError:
        print(f"Permission denied for writing to '{file_path}'.")


while True:
    display_menu()
    choice = input("Enter your choice (1-7): ")

    if choice == "1":
        directory = input("Enter directory path: ")
        list_files_and_directories(directory)
    elif choice == "2":
        directory = input("Enter directory name to create: ")
        create_directory(directory)
    elif choice == "3":
        path = input("Enter file or directory path to delete: ")
        delete_file_or_directory(path)
    elif choice == "4":
        src = input("Enter source path: ")
        dest = input("Enter destination path: ")
        rename_file_or_directory(src, dest)
    elif choice == "5":
        file_path = input("Enter file path to read: ")
        read_file_contents(file_path)
    elif choice == "6":
        file_path = input("Enter file path to write to: ")
        data = input("Enter data to write: ")
        write_to_file(file_path, data)
    elif choice == "7":
        break
    else:
        print("Invalid choice. Please select a valid option.")
