import tkinter as tk
from tkinter import messagebox

class TodoApp:
    def _init_(self, root):
        self.root = root
        self.root.title("To-Do List")
        
        self.tasks = []
        
        self.task_entry = tk.Entry(root, width=40)
        self.task_entry.pack(pady=10)
        
        self.add_button = tk.Button(root, text="Add Task", command=self.add_task)
        self.add_button.pack()
        
        self.task_listbox = tk.Listbox(root, width=40)
        self.task_listbox.pack(pady=10)
        
        self.remove_button = tk.Button(root, text="Remove Task", command=self.remove_task)
        self.remove_button.pack()
        
        self.quit_button = tk.Button(root, text="Quit", command=root.quit)
        self.quit_button.pack()
        
    def add_task(self):
        task = self.task_entry.get()
        if task:
            self.tasks.append(task)
            self.update_task_list()
            self.task_entry.delete(0, tk.END)
        else:
            messagebox.showwarning("Warning", "Please enter a task.")

    def remove_task(self):
        selected_task_index = self.task_listbox.curselection()
        if selected_task_index:
            index = selected_task_index[0]
            self.tasks.pop(index)
            self.update_task_list()

    def update_task_list(self):
        self.task_listbox.delete(0, tk.END)
        for task in self.tasks:
            self.task_listbox.insert(tk.END, task)

def main():
    root = tk.Tk()
    app = TodoApp(root)
    root.mainloop()

if _name_ == "_main_":
    main()
